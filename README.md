<!DOCTYPE html>
<html lang="pl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Szymon-Blog</title>
    <link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@400;700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
    
    <style>
        body { font-family: 'Montserrat', sans-serif; margin: 0; background-color: #f0f2f5; color: #1c1e21; }
        header { background: linear-gradient(135deg, #1a2a6c, #b21f1f, #fdbb2d); color: white; padding: 40px 20px; text-align: center; }
        nav { background: #0d1b2a; padding: 10px; text-align: center; position: sticky; top: 0; z-index: 1000; box-shadow: 0 2px 10px rgba(0,0,0,0.3); }
        nav a { color: white; margin: 5px 10px; padding: 10px 15px; text-decoration: none; font-weight: bold; display: inline-block; border-radius: 8px; transition: 0.3s; cursor: pointer; }
        nav a:hover { background: rgba(255,255,255,0.1); color: #fdbb2d; }
        
        .container { max-width: 800px; width: 95%; margin: 20px auto; padding: 20px; background: white; border-radius: 12px; box-shadow: 0 4px 15px rgba(0,0,0,0.1); min-height: 400px; box-sizing: border-box; }
        .scena { display: none; opacity: 0; transform: translateY(20px); transition: 0.6s cubic-bezier(0.22, 1, 0.36, 1); }
        .scena.aktywna { display: block; opacity: 1; transform: translateY(0); }
        
        /* POSTY */
        .post { border-bottom: 2px solid #eee; padding: 20px 0; margin-bottom: 20px; }
        .post-date { font-size: 0.85rem; color: #888; margin-bottom: 5px; display: block; font-weight: bold; }
        .heart-btn { background: none; border: none; color: #ccc; font-size: 1.4rem; cursor: pointer; transition: 0.3s; display: flex; align-items: center; gap: 8px; padding: 5px 0; outline: none; }
        .heart-btn.liked { color: #e74c3c; transform: scale(1.1); }

        /* KOMENTARZE */
        .comment-section { margin-top: 20px; border-top: 1px solid #f0f0f0; padding-top: 15px; }
        .comment-item { display: flex; gap: 10px; margin-bottom: 12px; align-items: flex-start; }
        .comment-avatar { width: 35px; height: 35px; background: #ddd; border-radius: 50%; display: flex; align-items: center; justify-content: center; font-size: 0.8rem; color: #666; flex-shrink: 0; }
        .comment-bubble { background: #f0f2f5; padding: 8px 15px; border-radius: 18px; font-size: 0.9rem; line-height: 1.4; max-width: 85%; }
        .comment-user { font-weight: bold; font-size: 0.85rem; display: block; margin-bottom: 2px; color: #b21f1f; }

        /* FORMULARZ KOMENTOWANIA */
        .comment-form { display: flex; flex-direction: column; gap: 8px; margin-top: 15px; }
        .name-input { padding: 8px 15px; border: 1px solid #ddd; border-radius: 20px; font-size: 0.8rem; width: 150px; outline: none; }
        .input-row { display: flex; gap: 10px; align-items: center; }
        .comment-input { flex: 1; padding: 10px 15px; border: 1px solid #ddd; border-radius: 25px; font-family: 'Montserrat', sans-serif; outline: none; }
        .comment-btn { background: #1a2a6c; color: white; border: none; width: 40px; height: 40px; border-radius: 50%; cursor: pointer; display: flex; align-items: center; justify-content: center; }
        .comment-btn:hover { background: #b21f1f; }

        /* PASJE */
        .pasje-lista { list-style: none; padding: 0; margin-top: 20px; }
        .pasje-lista li { background: #f8f9fa; margin: 10px 0; padding: 15px; border-radius: 10px; display: flex; align-items: center; gap: 15px; border-left: 5px solid #b21f1f; }
        
        .social-container { display: flex; justify-content: center; gap: 20px; flex-wrap: wrap; margin-top: 30px; }
        .social-icon { width: 65px; height: 65px; background: #222; color: white; border-radius: 50%; display: flex; align-items: center; justify-content: center; font-size: 26px; text-decoration: none; transition: 0.4s; }
        .social-icon:hover { transform: translateY(-8px) rotate(360deg); }
        .social-icon.ig:hover { background: #E1306C; }
        .social-icon.fb:hover { background: #4267B2; }
        .social-icon.tt:hover { background: #000; }
        footer { text-align: center; padding: 40px; color: #777; font-size: 0.9rem; }
    </style>
</head>
<body>

<header>
    <h1>Blog Szymona</h1>
    <p>Moje życie jak w bajce</p>
</header>

<nav>
    <a onclick="pokazScene('start')"><i class="fas fa-home"></i> Start</a>
    <a onclick="pokazScene('omnie')"><i class="fas fa-user"></i> O mnie</a>
    <a onclick="pokazScene('kontakt')"><i class="fas fa-share-alt"></i> Social</a>
</nav>

<div class="container">
    <div id="start" class="scena aktywna">
        <h2>Najnowsze wpisy</h2>
        
        <article class="post">
            <span class="post-date">15 marca 2026</span>
            <h3>Powrót od babci</h3>
            <p>Wróciłem od babci i jutro idę do szkoły.</p>
            <button class="heart-btn" id="btn-post-0" onclick="polub(0)">
                <i class="far fa-heart"></i> <span class="count">0</span>
            </button>
            <div class="comment-section">
                <div id="comments-0"></div>
                <div class="comment-form">
                    <input type="text" class="name-input" id="name-0" placeholder="Twoje imię...">
                    <div class="input-row">
                        <input type="text" class="comment-input" id="input-0" placeholder="Napisz komentarz...">
                        <button class="comment-btn" onclick="dodajKomentarz(0)"><i class="fas fa-paper-plane"></i></button>
                    </div>
                </div>
            </div>
        </article>

        <article class="post">
            <span class="post-date">14 marca 2026</span>
            <h3>Nowy blog</h3>
            <p>Stworzyłem właśnie tego bloga!</p>
            <button class="heart-btn" id="btn-post-1" onclick="polub(1)">
                <i class="far fa-heart"></i> <span class="count">0</span>
            </button>
            <div class="comment-section">
                <div id="comments-1"></div>
                <div class="comment-form">
                    <input type="text" class="name-input" id="name-1" placeholder="Twoje imię...">
                    <div class="input-row">
                        <input type="text" class="comment-input" id="input-1" placeholder="Napisz komentarz...">
                        <button class="comment-btn" onclick="dodajKomentarz(1)"><i class="fas fa-paper-plane"></i></button>
                    </div>
                </div>
            </div>
        </article>
    </div>

    <div id="omnie" class="scena">
        <h2>O mnie</h2>
        <p>Mam 12 lat, mieszkam pod Poznaniem i mam sporo pasji!</p>
        <ul class="pasje-lista">
            <li><i class="fas fa-utensils" style="color: #b21f1f;"></i> <strong>Gotowanie</strong> - uwielbiam eksperymentować w kuchni.</li>
            <li><i class="fas fa-code" style="color: #1a2a6c;"></i> <strong>Programowanie</strong> - uczę się tworzyć strony.</li>
            <li><i class="fas fa-gamepad" style="color: #fdbb2d;"></i> <strong>Gry komputerowe</strong> - bardzo lubię grać w wolnym czasie.</li>
        </ul>
    </div>

    <div id="kontakt" class="scena">
        <h2>Moje Social Media</h2>
        <div class="social-container">
            <a href="https://www.instagram.com/szymonn_mierzwa/" target="_blank" class="social-icon ig"><i class="fab fa-instagram"></i></a>
            <a href="https://www.facebook.com/profile.php?id=61560064245677" target="_blank" class="social-icon fb"><i class="fab fa-facebook-f"></i></a>
            <a href="https://www.tiktok.com/@szymonn_mierzwa" target="_blank" class="social-icon tt"><i class="fab fa-tiktok"></i></a>
        </div>
    </div>
</div>

<footer>&copy; 2026 Mój Blog</footer>

<script>
    function pokazScene(idSceny) {
        var sceny = document.getElementsByClassName('scena');
        for (var i = 0; i < sceny.length; i++) {
            sceny[i].classList.remove('aktywna');
            sceny[i].style.display = 'none';
        }
        var wybrana = document.getElementById(idSceny);
        wybrana.style.display = 'block';
        setTimeout(function() { wybrana.classList.add('aktywna'); }, 10);
        window.scrollTo(0, 0);
    }

    function polub(idPosta) {
        const btn = document.getElementById('btn-post-' + idPosta);
        const icon = btn.querySelector('i');
        const countSpan = btn.querySelector('.count');
        let currentCount = parseInt(countSpan.innerText);
        btn.classList.toggle('liked');
        if (btn.classList.contains('liked')) {
            currentCount++;
            icon.classList.replace('far', 'fas');
            localStorage.setItem('szymon_lajk_' + idPosta, 'tak');
        } else {
            currentCount--;
            icon.classList.replace('fas', 'far');
            localStorage.removeItem('szymon_lajk_' + idPosta);
        }
        countSpan.innerText = currentCount;
    }

    function dodajKomentarz(idPosta) {
        const nameInput = document.getElementById('name-' + idPosta);
        const textInput = document.getElementById('input-' + idPosta);
        const imie = nameInput.value.trim() || "Anonim";
        const tresc = textInput.value.trim();
        if (tresc === "") return;
        let zapisane = JSON.parse(localStorage.getItem('szymon_komentarze_v2_' + idPosta) || "[]");
        zapisane.push({ autor: imie, tekst: tresc });
        localStorage.setItem('szymon_komentarze_v2_' + idPosta, JSON.stringify(zapisane));
        textInput.value = "";
        wyswietlKomentarze(idPosta);
    }

    function wyswietlKomentarze(idPosta) {
        const lista = document.getElementById('comments-' + idPosta);
        let zapisane = JSON.parse(localStorage.getItem('szymon_komentarze_v2_' + idPosta) || "[]");
        lista.innerHTML = zapisane.map(k => `
            <div class="comment-item">
                <div class="comment-avatar"><i class="fas fa-user"></i></div>
                <div class="comment-bubble">
                    <span class="comment-user">${k.autor}</span>
                    ${k.tekst}
                </div>
            </div>
        `).join('');
    }

    window.onload = function() {
        for (let i = 0; i <= 1; i++) {
            const btn = document.getElementById('btn-post-' + i);
            if (localStorage.getItem('szymon_lajk_' + i) === 'tak') {
                btn.classList.add('liked');
                btn.querySelector('i').classList.replace('far', 'fas');
                btn.querySelector('.count').innerText = "1";
            }
            wyswietlKomentarze(i);
        }
    };
</script>

</body>
</html>
