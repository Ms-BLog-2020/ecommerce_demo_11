<template>
    <div>
        <head>
        <meta charset="utf-8">
        <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
        <link href="https://fonts.googleapis.com/css2?family=Noto+Serif+TC:wght@300&display=swap" rel="stylesheet">

        </head>
        <loading :active.sync="isLoading"></loading>
        <header id="event_page">
            
            <div class="container-fluid" id="event_page_container">
                <div class="event_img event_sakura a">
                <router-link to="/home" tag="div">
                <div class="logo"></div>
                </router-link>
                <h1 class="event_title event_title_sakura" id="event">櫻花祭<br/>限定<br/>品茶活動</h1>
                </div>
                <div class="event_img event_time b">
                <h3 class="event_title event_time_title" id="event">品茶活動時間</h3>
                <div class="time time_01"><i class="fa fa-caret-right" id="event"></i>
                    <p class="time_text" id="event">櫻花初開季 2021/1/16 - 2021/2/1</p>
                </div>
                <div class="time time_02"> <i class="fa fa-caret-right" id="event"> </i>
                    <p class="time_text" id="event">櫻花盛放季 2021/2/2 - 2021/2/28</p>
                </div>
                <div class="time time_03"><i class="fa fa-caret-right" id="event"></i>
                    <p class="time_text" id="event">櫻花收尾季 2021/3/1 - 2021/3/7</p>
                </div>
                </div>
                <div class="event_img event_top c">
                <h3 class="event_title class_title" id="event">茶道體驗<br/>工作坊</h3>
                <p class="class_intro" id="event">茶道精神與背後的文化之美是什麼? 想體驗茶道文化的人，絕對不能錯過這堂茶道體驗工作坊，從文化精神到實際體驗泡茶通通都包含在工作坊中囉!</p>
                </div>
                <div class="event_img event_middle d">
                    <h3 class="event_title class_title" id="event">午後<br/>品茶課</h3>
                    <p class="class_intro" id="event">茶道也有家常式的品茶之道，<br/>體驗在家也能自己泡茶的茶道吧!</p>
                </div>
                <div class="event_img event_bottom e">
                    <h3 class="event_title class_title" id="event">茶道入門<br/>工作坊</h3>
                    <p class="class_intro" id="event">從基礎的茶道基本知識到春、夏、秋、冬四季不同的茶道流程，通通都在這堂課教你。</p>
                </div>
                <div class="event_img event_rigister f">
                    <h3 class="event_title register_title" id="event">品茶活動<br/>優惠</h3>
                    <p class="register_intro" id="event">心動不如馬上行動!<br/>想體驗正統茶道, 立即報名即可享受!!<br/>把握限定在櫻花季開放的品茶體驗活動吧!!</p>
                    <router-link to="/home_coupon" tag="div">
                    <button class="btn-outline-light register">
                    馬上領取優惠
                    </button>
                    </router-link>
                </div>
                <div class="event_img event_record g">
                <h3 class="event_title record_title" id="event">品茶活動<br/>花絮</h3>
                <video id="myEvent" autoplay="" muted="" loop="">
                    <source src="https://i.imgur.com/VPKPlXn.mp4"/>
                </video>
                </div>
            </div>
            </header>
            
            <section id="event_intro">
            <section id="video">
                <video id="myVideo" autoplay="" muted="" loop="">
                    <source src="https://i.imgur.com/BDNpgSJ.mp4" type="video/mp4"/>
                </video>
                <embed src="" autostart="true" loop="true" width="2" height="0"/>
            </section>
            <div class="container-fluid" id="event_page_container">
                <div class="row" id="event_page">
                
                    <div class="col-md-4 event_intro" id="event">
                    <img class="people" id="logo_event_intro" src="@/assets/images/eventpage_people.png"/>
                        <h3 class="event_intro" id="intro">小班制體驗</h3>
                        <p class="event_intro_content" id="event">每一堂課程皆有活動人數限定,讓您的品茶能夠有最佳品質體驗與感受! 每個人也都配有專屬的一套茶具,防疫期間可安心使用!趕快來報名體驗吧!!</p>
                    </div>
                    <div class="col-md-4 event_intro" id="event">
                    <img class="tradition" id="logo_event_intro" src="@/assets/images/eventpage_tradition.png"/>
                        <h3 class="event_intro" id="intro">傳統正宗</h3>
                        <p class="event_intro_content" id="event">茶道老師均為日本傳統茶道裹千家流派的正宗弟子, 讓您體驗到最正宗的日本茶道精神! 只要跟著老師的腳步, 您就能一步步體會到日本茶道之妙!!</p>
                    </div>
                    <div class="col-md-4 event_intro" id="event">
                    <img class="season" id="logo_event_intro" src="@/assets/images/eventpage_time.png"/>
                        <h3 class="event_intro" id="intro">最佳時節</h3>
                        <p class="event_intro_content" id="event">茶道在不同時節都有些微差異的流程, 但在櫻花時節絕對是體驗茶道的最佳季節!!在這櫻雪紛飛的盛放中, 一邊品茶一邊賞櫻, 何不樂哉!!</p>
                    </div>
                </div>
                <div class="col-md-12" id="register_bottom"> 
                    <router-link to="/home" tag="div">
                    <button class="btn-outline-light register_bottom">馬上報名</button>
                    </router-link>
                </div>
                
                
            </div>
            </section>
            

    </div>
</template>


<script>
    
    export default {
        data() {
            return{
                isLoading: false,
            }
        },
        mounted() {
            
            var video = document.getElementById("myEvent");
            var video_02 = document.getElementById("myVideo");
            
            
            },
            
        };

</script>

<style>
    * {
        font-family: 'Noto Serif JP','Noto Serif TC';
    }

    html.skrollr.skrollr-desktop {
        max-width: 1520px;
        overflow-x: hidden;
    }
    header#event_page  {
    min-height: 980px;
    max-width: 1520px;
    overflow-x: hidden;
    }
    .container-fluid#event_page_container {
        max-width: 1520px;
        overflow-x: hidden;
    }
    header#event_page .container-fluid {
        margin: 0px;
        padding: 0px;
        color: rgba(255, 255, 255, 0.5);
        min-height: 900px;
        display: grid;
        grid-template-rows: repeat(3, 1fr);
        grid-template-columns: repeat(5, 1fr);
        grid-template-areas: "a a c f f" "a a d g g" "b b e g g";
    }
    header#event_page .container-fluid .event_sakura.a {
        grid-area: a;
        background-image: linear-gradient(rgba(0, 0, 0, 0.2), rgba(0, 0, 0, 0.3)), url("https://i.imgur.com/nGlMZR9.jpg");
        background-size: auto 105%;
        transition-duration: 2s;
    }
    header#event_page .container-fluid .event_sakura.a:hover {
        background-size: auto 115%;
        filter: brightness(1.3);
    }
    header#event_page .container-fluid .event_sakura.a .event_title_sakura {
        font-size: 72px;
        line-height: 100px;
        color: white;
        text-shadow: 5px 5px 20px black;
    }
    header#event_page .container-fluid .event_sakura.a .logo {
        padding: 50px;
        margin-bottom: 30px;
        width: 50px;
        background-image: url(https://i.imgur.com/BCXtjMv.png);
        background-size: cover;
        cursor: pointer;
    }
    header#event_page .container-fluid .event_time.b {
        grid-area: b;
        background-image: linear-gradient(rgba(0, 0, 0, 0.3), rgba(0, 0, 0, 0.1)), url("https://i.imgur.com/5YPzJW9.jpg");
        background-size: auto 101%;
        transition-duration: 2s;
    }
    header#event_page .container-fluid .event_time.b:hover {
        background-size: auto 115%;
        filter: brightness(1.2);
    }
    header#event_page .container-fluid .event_time.b:hover h3#event {
        text-shadow: 3px 3px 11px black;
        color: white;
    }
    header#event_page .container-fluid .event_time.b:hover p#event {
        opacity: 1;
        text-shadow: 3px 3px 11px black;
        color: white;
    }
    header#event_page .container-fluid .event_time.b:hover i#event {
        opacity: 1;
        text-shadow: 5px 5px 11px black;
        color: white;
    }
    header#event_page .container-fluid .event_time.b .time {
        padding-bottom: 10px;
    }
    header#event_page .container-fluid .event_time.b .time_text, header#event_page .container-fluid .event_time.b i#event {
        display: inline-block;
    }
    header#event_page .container-fluid .event_top.c {
    grid-area: c;
    background-image: linear-gradient(rgba(0, 0, 0, 0.5), rgba(0, 0, 0, 0.1)), url("https://i.imgur.com/4FSMcqF.jpg");
    background-size: auto 105%;
    transition-duration: 2s;
    }
    header#event_page .container-fluid .event_top.c:hover {
    background-size: auto 115%;
    filter: brightness(1.3);
    }
    header#event_page .container-fluid .event_top.c:hover h3#event {
    text-shadow: 3px 3px 11px black;
    color: white;
    }
    header#event_page .container-fluid .event_top.c:hover p#event {
    opacity: 1;
    text-shadow: 3px 3px 11px black;
    color: white;
    }
    header#event_page .container-fluid .event_middle.d {
    grid-area: d;
    background-image: linear-gradient(rgba(0, 0, 0, 0.5), rgba(0, 0, 0, 0.1)), url("https://i.imgur.com/KWuXMmI.jpg");
    background-size: auto 105%;
    transition-duration: 2s;
    }
    header#event_page .container-fluid .event_middle.d:hover {
    background-size: auto 115%;
    filter: brightness(1.3);
    }
    header#event_page .container-fluid .event_middle.d:hover h3#event {
    text-shadow: 3px 3px 11px black;
    color: white;
    }
    header#event_page .container-fluid .event_middle.d:hover p#event {
    opacity: 1;
    text-shadow: 3px 3px 11px black;
    color: white;
    }
    header#event_page .container-fluid .event_bottom.e {
    grid-area: e;
    background-image: linear-gradient(rgba(0, 0, 0, 0.4), rgba(0, 0, 0, 0.2)), url("https://i.imgur.com/4xXmkGQ.jpg");
    background-size: auto 105%;
    transition-duration: 2s;
    }
    header#event_page .container-fluid .event_bottom.e:hover {
    background-size: auto 115%;
    filter: brightness(1.2);
    }
    header#event_page .container-fluid .event_bottom.e:hover h3#event {
    text-shadow: 3px 3px 11px black;
    color: white;
    }
    header#event_page .container-fluid .event_bottom.e:hover p#event {
    opacity: 1;
    text-shadow: 3px 3px 11px black;
    color: white;
    }
    header#event_page .container-fluid .event_rigister.f {
    grid-area: f;
    background-image: linear-gradient(rgba(0, 0, 0, 0.5), rgba(0, 0, 0, 0.1)), url("https://i.imgur.com/nZg7r9q.jpg");
    background-size: auto 105%;
    transition-duration: 2s;
    }
    header#event_page .container-fluid .event_rigister.f:hover {
    background-size: auto 115%;
    filter: brightness(1.4);
    }
    header#event_page .container-fluid .event_rigister.f:hover h3#event {
    text-shadow: 3px 3px 11px black;
    color: white;
    }
    header#event_page .container-fluid .event_rigister.f:hover p#event {
    opacity: 1;
    text-shadow: 3px 3px 11px black;
    color: white;
    }
    header#event_page .container-fluid .event_rigister.f:hover p#event, header#event_page .container-fluid .event_rigister.f:hover button.btn-outline-light.register {
    opacity: 1;
    color: white;
    }
    header#event_page .container-fluid .event_rigister.f button.btn-outline-light.register {
    margin-top: 18px;
    background-color: transparent;
    border: solid 2px white;
    border-radius: 30px;
    font-size: 16px;
    transition-duration: 0.5s;
    letter-spacing: 2px;
    padding: 5px 30px;
    opacity: 0;
    }
    header#event_page .container-fluid .event_rigister.f button.btn-outline-light.register:hover {
    background-color: white;
    color: gray;
    font-weight: 700;
    }
    header#event_page .container-fluid .event_record.g {
    grid-area: g;
    overflow: hidden;
    padding: 0px;
    }
    header#event_page .container-fluid .event_record.g video#myEvent {
    bottom: 0px;
    right: 0px;
    transform: scale(1.7);
    filter: brightness(0.5);
    transition-duration: 2s;
    }
    header#event_page .container-fluid .event_record.g video#myEvent:hover {
    filter: brightness(1.2);
    }
    header#event_page .container-fluid .event_record.g video#myEvent:hover h3#event {
    text-shadow: 3px 3px 11px black;
    color: white;
    }
    header#event_page .container-fluid .event_record.g h3#event {
    position: relative;
    z-index: 11;
    top: 30px;
    left: 30px;
    }
    header#event_page .container-fluid .a, header#event_page .container-fluid .b, header#event_page .container-fluid .c, header#event_page .container-fluid .d, header#event_page .container-fluid .e, header#event_page .container-fluid .f, header#event_page .container-fluid .g {
    padding: 30px;
    }
    header#event_page .container-fluid .event_title {
    padding: 0px;
    padding-bottom: 22px;
    margin: 0px;
    line-height: 45px;
    }
    header#event_page .container-fluid h3#event {
    font-size: 36px;
    transition-duration: 2s;
    }
    header#event_page .container-fluid p#event {
    font-size: 16px;
    line-height: 25px;
    opacity: 0;
    transition-duration: 1s;
    }
    header#event_page .container-fluid i#event {
    opacity: 0;
    }

    section#video #myVideo {
        right: 0;
        bottom: 0;
        min-width: 100%;
        min-height: 100%;
    }

    section#event_intro {
    overflow-x: hidden;    
    max-width: 1520px;
    background-image: linear-gradient(rgba(0, 0, 0, 0.1), rgba(0, 0, 0, 0.5)), url("https://i.imgur.com/oFJQ7XC.jpg");
    background-attachment: fixed;
    background-size: cover;
    min-height: 850px;
    margin: 0px;
    color: white;
    text-align: center;
    display: block;
    vertical-align: top;
    
    }
    section#event_intro button.btn-outline-light.register_bottom {
        background-color: transparent;
        border: solid 2px white;
        border-radius: 40px;
        font-size: 28px;
        padding: 10px 40px;
        margin-bottom: 50px;
        letter-spacing: 5px;
        transition-duration: 0.5s;
    }
    section#event_intro button.btn-outline-light.register_bottom:hover {
    background-color: white;
    color: gray;
    }
    section#event_intro .container-fluid {
    margin: 10px;
    }
    section#event_intro .container-fluid .event_intro {
    padding: 50px;
    
    }
    section#event_intro .container-fluid .event_intro h3#intro {
    padding: 0px;
    padding-bottom: 30px;
    font-size: 32px;
    }
    section#event_intro .container-fluid .event_intro p#event {
    font-size: 16px;
    line-height: 35px;
    text-align-last: left;
    padding-bottom: 60px;
    }
    section#event_intro .container-fluid .people, section#event_intro .container-fluid .tradition, section#event_intro .container-fluid .season {
    opacity: 0.8;
    transition-duration: 0.5s;
    padding-bottom: 20px;
    }
    section#event_intro .container-fluid .people:hover, section#event_intro .container-fluid .tradition:hover, section#event_intro .container-fluid .season:hover {
    opacity: 1;
    animation: rotating 2s both;
    }

    @keyframes rotating {
    0% {
        transform: rotate(0deg);
    }
    25% {
        transform: rotate(10deg);
    }
    50% {
        transform: rotate(-10deg);
    }
    100% {
        transform: rotate(0deg);
    }
    }
    @media screen and (max-width: 768px) {
    header#event_page  {
    min-height: 2800px;
    }
    header#event_page .container-fluid {
        min-height: 300px;
        grid-template-rows: repeat(3, 1fr);
        grid-template-columns:50%;
        grid-template-areas: "a a""b b""c c""d e""f f""g g";
    }
    section#event_intro {
        display: none;
    }
    }
</style>