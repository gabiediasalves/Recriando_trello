<template>
  <div id="app">
   <headerView/>
   <div class="board">
  <div class="lane">
      <h2 class="lane-title">Backlog</h2>
      <Container group-name="trello" 
      @drag-start="handleDragStart('backlog', $event)" 
      @drop="handleDrop('backlog', $event)"
      :get-child-payload="getChildPayload"
      :drop-placeholder="{className: 'placeholder'}">
        <Draggable v-for="card in cards.backlog" :key="card.id">
      <cardView >{{card.text}}</cardView>
       </Draggable>
      </Container>
 </div>
  <div class="lane">
      <h2 class="lane-title">Desenvolvimento</h2>
       <Container group-name="trello" 
       @drag-start="handleDragStart('dev', $event)" 
       @drop="handleDrop('dev', $event)"
       :get-child-payload="getChildPayload"
       :drop-placeholder="{className: 'placeholder'}">
        <Draggable v-for="card in cards.dev" :key="card.id">
      <cardView >{{card.text}}</cardView>
       </Draggable>
      </Container>
  </div>
  <div class="lane">
      <h2 class="lane-title">Teste</h2>
      <Container group-name="trello" 
      @drag-start="handleDragStart('testes', $event)" 
      @drop="handleDrop('testes', $event)"
      :get-child-payload="getChildPayload"
      :drop-placeholder="{className: 'placeholder'}">
        <Draggable v-for="card in cards.testes" :key="card.id">
      <cardView >{{card.text}}</cardView>
       </Draggable>
      </Container>
  </div>
  <div class="lane">
      <h2 class="lane-title">Concluido</h2>
       <Container group-name="trello" 
       @drag-start="handleDragStart('fechados', $event)" 
       @drop="handleDrop('fechados', $event)"
       :get-child-payload="getChildPayload"
       :drop-placeholder="{className: 'placeholder'}">
        <Draggable v-for="card in cards.fechados" :key="card.id">
      <cardView >{{card.text}}</cardView>
       </Draggable>
      </Container>
  </div>
   </div>
  </div>
</template>

<script>
import headerView from './components/headerView';
import cardView from './components/cardView';
import initialCards from './initialCards';
import {Container, Draggable} from "vue-smooth-dnd";
export default {
  name: 'App',
  components:{
    headerView,
    cardView,
    Container, 
    Draggable,
  },
  data:() => ({
    cards: {
      backlog: initialCards.backlog,
      dev: initialCards.dev,
      testes: initialCards.testes,
      fechados: []
    },
    draggingCard:{
      lane: '',
      index: -1,
      cardData: {}
    }
  }),
  methods:{
    handleDragStart(lane, dragResult){
      const {payload, isSource} = dragResult
      if(isSource){
        this.draggingCard = {
          lane,
          index: payload.index,
          cardData:{
            ...this.cards[lane][payload.index]
          }
        }
      }

    },
    handleDrop(lane, dropResult){
      const {removedIndex, addedIndex} = dropResult
     if(lane ===this.draggingCard.lane && removedIndex === addedIndex){
       return
     }
     if(removedIndex!== null){
       this.cards[lane].splice(removedIndex, 1)
     }
      if(addedIndex !== null)
      this.cards[lane].splice(addedIndex, 0, this.draggingCard.cardData)
    },
    getChildPayload(index){
      return{
        index
      }
    }
  }
}
</script>

<style>
.board{
  display: flex;
  justify-content: flex-start;
  margin: 1.2rem 0.8rem;
  align-items: flex-start;
}

.lane{
  background: var(--color-gray);
  width: 23rem;
  border-radius: 0.8rem;
  box-shadow: 0 .1rem .2rem 0 rgba(33,33,33, 0.1rem); 
  margin: 0 0.8rem;
  padding : 0 0.7rem;

}

.lane-title{
  margin-bottom: 0.6rem;
  padding: 0.8rem 0.5rem;
}
.placeholder{
  background: rgba(33,33,33, 0.08);
  border-radius:0.4rem;
  transform: scaleY(0.85);
  transform-origin: 0% 0%;
}
</style>
