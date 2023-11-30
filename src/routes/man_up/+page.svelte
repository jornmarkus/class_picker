<script>
const  classes=[ ['Shaman', 'rgba(35, 89, 255, 0.85)', '100px, 100px'],
        ['Rogue','rgba(255, 244, 104, 0.85)', '0, 100px'], //<- first class
        ['Druid','rgba(255, 124, 10, 0.85)', '-100px, 100px'],
        ['Warrior','rgba(198, 155, 109, 0.85)', '100px, 0'],
        ['Mage','rgba(63, 199, 235, 0.85)', '0, 0'],
        ['Priest','rgba(255,255,255, 0.85)', '-100px, 0'],
        ['Warlock','rgba(147, 130, 201, 0.85)', '100px, -100px'],
        ['Paladin','rgba(244, 140, 186, 0.85)', '0, -100px'],
        ['Hunter','rgba(170, 211, 114, 0.85)', '-100px, -100px'],
]
    const chosen = Math.floor(Math.random() * classes.length);
    const [chosen_class, color] = classes[chosen];
    function select_class(e, translation_to_center){
        e.target.id = 'the_chosen_one';
        e.target.style.transform = `translate(${translation_to_center})`
        const client_rect = e.target.getBoundingClientRect();
        const x = client_rect.x;
        const y = client_rect.y;
       document.getElementById('header').style.display = 'none'
       const class_cards =  document.getElementsByClassName('class_card')
         for (let i = 0; i < class_cards.length; i++) {
              if(class_cards[i].id !== 'the_chosen_one'){
                   const my_rect =  class_cards[i].getBoundingClientRect()
                    const my_x = my_rect.x
                    const my_y = my_rect.y
                    let my_new_x = Math.random() * 20 + 60 //vw
                    let my_new_y = Math.random() * 20 + 60 //vh
                    my_new_x = Math.random() > 0.5 ? my_new_x * -1 : my_new_x
                    my_new_y = Math.random() > 0.5 ? my_new_y * -1 : my_new_y
                    class_cards[i].style.transform = `translate(${my_new_x}vw, ${my_new_y}vh)`
                    class_cards[i].style.transition = 'all 1s'
                       // * 200 + (50 * i)}px, ${Math.random() * 100 - 50}vh)`
              }
              //class_cards[i].id = '';
         }
        console.log(e)
        blast()
    }
    function blast(){
        const the_true_chosen = Math.floor(Math.random() * 9)
        
        const class_cards =  document.getElementsByClassName('class_card')
        for (let i = 0; i < class_cards.length; i++) {
            const current_chosen = document.getElementById('the_chosen_one')
            if(class_cards[i].id !== 'the_chosen_one'){
                setTimeout(() => {
                    if(the_true_chosen === i){
                        setTimeout(() => {
                            //const loser = document.getElementById('the_chosen_one')
                            current_chosen.id = ''
                            current_chosen.style.transform = `translate(${Math.random() * 100 + 100}vw, ${Math.random() * 100 + 100}vh)`
                            current_chosen.style.opacity= '0'
                            current_chosen.style.transition = 'all 1s'
                        }, 500);
                        class_cards[i].id = 'the_chosen_one'
                        class_cards[i].style.transform = `translate(${classes[i][2]})`
                    }else{
                        class_cards[i].classList.add('loser')
                        class_cards[i].style.transform = `translate(${classes[i][2]})`
                        class_cards[i].style.transition = 'all 1s'
                    }
                }, 1500 + i * 1000);
            }
        }
    
    }
</script>
 <style>
 h1{
    color: white;
 }
 :global(body){
    background: #292f36;
    
 }

 button{
        border: none;
        cursor: pointer;
        outline: none;
        border: 2px solid white;
        font-size: 24px;
        color: black;
 }
 :global(#the_chosen_one){
    z-index: 999;
    width: 200px !important;
    height: 200px !important;
    transition: all .5s linear;
    border: 5px solid gold;
    position: relative;
 }
 :global(.loser){
    animation: loser 1s linear;
    animation-fill-mode: forwards;
 }

 @keyframes loser{
    0% {opacity: 1;}
    80% {opacity: 0.7;}
    99% {opacity: 0.2;}
    100% {opacity: 0;}
}
 @keyframes chosen{
        from{top: 50vh; left: -200px;}
        to{top: 50vh; left: 50vw;}
 }
 .class_card{
        width: 100px;
        height: 100px;
        border-radius: 4px;
        display: inline-flex;
        justify-content: center;
        align-items: center;
        flex-shrink: 0;
        color: white;
        margin: 8px;
        font-weight: 500;
    }
 #class_selector{
        justify-items: center;
        justify-content: center;
 }
 .outer_cont{
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        height: 95vh;
        overflow: hidden;
 }
 </style>
<!--
<div  id='the_chosen_one' class='class_card ' style='background: {color}'>
    <p> {chosen_class}</p>
</div>
-->
<div class='outer_cont'>

<h1 id='header'>CHOOSE YOUR CLASS</h1>
<div id='class_selector'>
    {#each classes as [class_name, class_color, translation_to_center], n }
        {#if n % 3 === 0}
            <br>
        {/if}
        <button class='class_card' style='background-color: {class_color}'
        on:click={(e) =>{select_class(e, translation_to_center)}}>
            {class_name}
</button>
    {/each}
</div>
</div>