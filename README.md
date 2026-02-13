<!DOCTYPE html>  <html lang="en">  
<head>  
    <meta charset="UTF-8">  
    <meta name="viewport" content="width=device-width, initial-scale=1.0">  
    <title>Be My Valentine?</title>  
    <style>  
        :root {  
            --soft-pink: #ffe4e9;  
            --deep-pink: #ffafbd;  
            --accent-red: #ff4d6d;  
            --white: #ffffff;  
        }  body {  
        margin: 0;  
        padding: 0;  
        display: flex;  
        justify-content: center;  
        align-items: center;  
        min-height: 100vh;  
        font-family: 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;  
        background: linear-gradient(135deg, var(--soft-pink) 0%, var(--white) 100%);  
        overflow: hidden;  
        text-align: center;  
    }  

    /* Floating Hearts Background */  
    .background-elements {  
        position: fixed;  
        top: 0;  
        left: 0;  
        width: 100%;  
        height: 100%;  
        pointer-events: none;  
        z-index: 0;  
    }  

    .heart-float {  
        position: absolute;  
        color: var(--accent-red);  
        opacity: 0.3;  
        animation: float 6s infinite ease-in-out;  
    }  

    @keyframes float {  
        0% { transform: translateY(100vh) scale(0); opacity: 0; }  
        50% { opacity: 0.5; }  
        100% { transform: translateY(-10vh) scale(1.5); opacity: 0; }  
    }  

    /* Main Container */  
    .container {  
        position: relative;  
        z-index: 10;  
        background: rgba(255, 255, 255, 0.8);  
        backdrop-filter: blur(10px);  
        padding: 3rem 2rem;  
        border-radius: 30px;  
        box-shadow: 0 15px 35px rgba(255, 175, 189, 0.3);  
        max-width: 400px;  
        width: 90%;  
        border: 1px solid rgba(255, 255, 255, 0.5);  
    }  

    .heart-icon {  
        font-size: 4rem;  
        color: var(--accent-red);  
        margin-bottom: 1rem;  
        display: block;  
        animation: pulse 1.5s infinite;  
    }  

    @keyframes pulse {  
        0% { transform: scale(1); }  
        50% { transform: scale(1.1); }  
        100% { transform: scale(1); }  
    }  

    h1 {  
        color: #4a4a4a;  
        font-weight: 300;  
        font-size: 1.8rem;  
        margin-bottom: 2rem;  
        line-height: 1.4;  
    }  

    /* Buttons */  
    .btn-group {  
        display: flex;  
        justify-content: center;  
        gap: 20px;  
        align-items: center;  
        height: 60px;  
    }  

    .btn {  
        padding: 12px 35px;  
        font-size: 1.1rem;  
        border: none;  
        border-radius: 50px;  
        cursor: pointer;  
        transition: all 0.3s ease;  
        font-weight: 600;  
        outline: none;  
    }  

    #yesBtn {  
        background-color: var(--accent-red);  
        color: white;  
        box-shadow: 0 5px 15px rgba(255, 77, 109, 0.4);  
        animation: bounce 2s infinite;  
    }  

    #yesBtn:hover {  
        transform: scale(1.1);  
        box-shadow: 0 0 20px rgba(255, 77, 109, 0.6);  
    }  

    #noBtn {  
        background-color: #f0f0f0;  
        color: #888;  
        position: relative;  
    }  

    @keyframes bounce {  
        0%, 20%, 50%, 80%, 100% {transform: translateY(0);}  
        40% {transform: translateY(-10px);}  
        60% {transform: translateY(-5px);}  
    }  

    /* Final Screen */  
    .hidden { display: none; }  
      
    .success-msg {  
        font-size: 1.5rem;  
        color: var(--accent-red);  
        font-weight: bold;  
    }  

</style>

</head>  
<body>  <div class="background-elements" id="bg"></div>  

<div class="container" id="mainCard">  
    <span class="heart-icon">❤️</span>  
    <h1 id="question">Shireen mam, <br>Will you be my Valentine? ❤️</h1>  
      
    <div class="btn-group">  
        <button class="btn" id="yesBtn" onclick="celebrate()">YES</button>  
        <button class="btn" id="noBtn" onmouseover="moveButton()" onclick="moveButton()">NO</button>  
    </div>  
</div>  

<div class="container hidden" id="successCard">  
    <span class="heart-icon">💖</span>  
    <p class="success-msg">You just made my day! ❤️</p>  
</div>  

<script>  
    // Create falling hearts/petals  
    const bg = document.getElementById('bg');  
    const colors = ['#ffafbd', '#ffc3a0', '#ff4d6d', '#ffffff'];  

    function createPetal() {  
        const petal = document.createElement('div');  
        petal.innerHTML = '🌸'; // Can switch to '❤️' for hearts  
        petal.className = 'heart-float';  
        petal.style.left = Math.random() * 100 + 'vw';  
        petal.style.fontSize = (Math.random() * 20 + 10) + 'px';  
        petal.style.animationDuration = (Math.random() * 3 + 4) + 's';  
        bg.appendChild(petal);  

        setTimeout(() => { petal.remove(); }, 6000);  
    }  

    setInterval(createPetal, 300);  

    // Playful NO button logic  
    function moveButton() {  
        const noBtn = document.getElementById('noBtn');  
        const x = Math.random() * (window.innerWidth - noBtn.offsetWidth);  
        const y = Math.random() * (window.innerHeight - noBtn.offsetHeight);  
          
        noBtn.style.position = 'fixed';  
        noBtn.style.left = x + 'px';  
        noBtn.style.top = y + 'px';  
          
        // Randomly change text for fun  
        const phrases = ["Are you sure?", "Think again!", "Puh-lease?", "Wrong button!", "Nice try!"];  
        noBtn.innerText = phrases[Math.floor(Math.random() * phrases.length)];  
    }  

    // YES button logic  
    function celebrate() {  
        document.getElementById('mainCard').classList.add('hidden');  
        document.getElementById('successCard').classList.remove('hidden');  
          
        // Extra burst of hearts  
        for(let i=0; i<50; i++) {  
            setTimeout(createPetal, i * 50);  
        }  
    }  
</script>

</body>  
</html>
