<template>
  <header class="headerView">
    <nav>
      <a class="navbar" href="#">Trello</a>
      <details>
      <summary></summary>
        <div class="menu">
          <a href="#">Fundo</a>
          <a href="#link">Work</a>
          <a href="#link">Links</a>
        </div>
      </details>
    </nav>
  </header>
</template>

<script>
export default{
    name: 'headerView'
  }
</script>

<style scoped>
.headerView{
  width: 100%;
  background: var(--color-main);
  height:45px;
}
nav{
  display: flex;
  color: var(--color-white);
  justify-content: space-between;
  
  
}
.navbar{
  font-size: 23px;
  text-decoration: none;
  color: var(--color-white);
  margin-left: 10px;
  }




details {
  padding:6px;
  margin-right: 30px;
}
summary {
  writing-mode: vertical-lr;
  text-align: center;
  padding: 12px 6px;
  width: 23px;
  height: 17px;
  cursor: pointer;
  
}
summary::after {
  content: "III";
  letter-spacing: -1px;
  font-size: 15px;
}
summary:hover {
  transform: scale(1.1);
}
summary::marker {
  font-size: 0;
}
details[open] .menu {
  animation-name: menuAnim;
}
details[open] summary::before {
  content: "X";
  font-size: 15px;
}
details[open] summary::after {
  content: "";
}
.menu {
  box-shadow: 0 4px 12px 0 rgba(0, 0, 0, 0.2);
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  overflow: hidden;
  animation: closeMenu 300ms ease-in-out forwards;
}
.menu a {
  padding: 10px;
  margin: 0 16px;
  color: white;
  border-bottom: 2px solid rgba(0, 0, 0, 0.1);
  text-decoration: none;
  text-align: center;
  transition: filter 200ms linear 0s;
}

@keyframes menuAnim {
  0% {
    height: 0;
  }
  100% {
    height: 150px;
  }
}
@keyframes fadeMe {
  0% {
    opacity: 0.4;
  }
  100% {
    opacity: 0;
  }
}




</style>