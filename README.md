# halloween's game
<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Sceau I — La malédiction des sceaux</title>
<style>
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  body {
    height: 100vh;
    overflow: hidden;
    font-family: Georgia, serif;
    color: #e8e2d0;
    background: #05070a;
  }

  .background {
    position: fixed;
    inset: 0;
    z-index: -2;
    background:
      radial-gradient(circle at 20% 20%, rgba(40, 80, 40, 0.35), transparent 45%),
      radial-gradient(circle at 80% 80%, rgba(20, 60, 30, 0.35), transparent 50%),
      linear-gradient(180deg, #0b1410 0%, #05070a 70%);
  }

  .plants {
    position: fixed;
    inset: 0;
    z-index: -1;
    opacity: 0.25;
    background-image:
      radial-gradient(circle at 10% 90%, #14351f 0 12%, transparent 13%),
      radial-gradient(circle at 25% 95%, #0f2a18 0 15%, transparent 16%),
      radial-gradient(circle at 85% 90%, #123020 0 14%, transparent 15%),
      radial-gradient(circle at 70% 100%, #0d2415 0 18%, transparent 19%);
    filter: blur(2px);
  }

  .vignette {
    position: fixed;
    inset: 0;
    z-index: 0;
    background: radial-gradient(circle at 35% 50%, transparent 25%, rgba(0, 0, 0, 0.88) 85%);
    pointer-events: none;
  }

  .scene {
    position: relative;
    z-index: 1;
    height: 100%;
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 4vw;
    gap: 2rem;
  }

  .text-zone {
    width: 60%;
    max-width: 700px;
  }

  h1 {
    font-size: clamp(2rem, 5vw, 3.5rem);
    color: #d8b45a;
    letter-spacing: 0.2em;
    text-shadow: 0 0 18px rgba(216, 180, 90, 0.5);
    margin-bottom: 2rem;
  }

  .oscar-text {
    font-size: clamp(1.05rem, 2.1vw, 1.5rem);
    line-height: 1.7;
    min-height: 45vh;
    white-space: pre-wrap;
    text-shadow: 0 2px 8px rgba(0, 0, 0, 0.9);
  }

  .skeleton-zone {
    width: 30%;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
  }

  .skeleton {
    font-size: clamp(90px, 18vw, 220px);
    filter: drop-shadow(0 0 25px rgba(0, 0, 0, 0.9));
    animation: float 5s ease-in-out infinite;
  }

  .skeleton-name {
    margin-top: 0.5rem;
    color: #d8b45a;
    letter-spacing: 0.25em;
    text-transform: uppercase;
  }

  button {
    margin-top: 2rem;
    padding: 0.9rem 1.8rem;
    background: transparent;
    color: #d8b45a;
    border: 1px solid #d8b45a;
    font-family: inherit;
    font-size: 1rem;
    letter-spacing: 0.15em;
    cursor: pointer;
    transition: all 0.3s ease;
  }

  button:hover {
    background: #d8b45a;
    color: #05070a;
    box-shadow: 0 0 25px rgba(216, 180, 90, 0.5);
  }

  .hidden {
    display: none;
  }

  @keyframes float {
    0%, 100% {
      transform: translateY(0);
    }
    50% {
      transform: translateY(-12px);
    }
  }

  @media (max-width: 750px) {
    .scene {
      flex-direction: column;
      justify-content: center;
      padding: 1.5rem;
    }

    .text-zone {
      width: 100%;
      order: 2;
    }

    .skeleton-zone {
      width: 100%;
      order: 1;
    }

    .oscar-text {
      min-height: 35vh;
    }
  }
</style>
</head>
<body>

<div class="background"></div>
<div class="plants"></div>
<div class="vignette"></div>

<main class="scene">
  <section class="text-zone">
    <h1>Sceau I</h1>
    <p id="oscar-text" class="oscar-text"></p>
    <button id="next-btn" class="hidden">Entrer dans la première épreuve</button>
  </section>

  <aside class="skeleton-zone">
    <div class="skeleton">💀</div>
    <p class="skeleton-name">Oscar</p>
  </aside>
</main>

<script>
  const text = `Bonjour, je suis Oscar, le squelette en charge de l’accueil des candidats à l’examen d’entrée de la fête des monstres d’Halloween.

Je sais, c’est nul comme job, mais bon… je suis nouveau. Je me suis échappé d’une salle de SVT il y a deux semaines.

L’examen se déroule en 8 étapes. Vous avez 30 minutes.

Je vous rappelle que les montres connectées sont interdites.

La première épreuve commence maintenant.

Bon courage !`;

  const textElement = document.getElementById("oscar-text");
  const nextButton = document.getElementById("next-btn");

  let index = 0;
  let deleting = false;

  function typeEffect() {
    if (!deleting) {
      textElement.textContent = text.slice(0, index);
      index++;

      if (index > text.length) {
        deleting = true;
        setTimeout(typeEffect, 5000);
        return;
      }

      setTimeout(typeEffect, 35);
    } else {
      index -= 8;
      textElement.textContent = text.slice(0, Math.max(index, 0));

      if (index <= 0) {
        nextButton.classList.remove("hidden");
        return;
      }

      setTimeout(typeEffect, 15);
    }
  }

  typeEffect();

  nextButton.addEventListener("click", () => {
    alert("Fin du Sceau I. La suite arrive bientôt !");
  });
</script>

</body>
</html>
