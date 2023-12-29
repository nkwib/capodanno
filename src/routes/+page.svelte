<script>
  import { onMount } from "svelte";
  import { Button } from "$lib/components/ui/button";

  let domande = [
    {
      q: "Preferisci la lasagna o il cotechino?",
      a: "lasagna",
      b: "cotechino",
      c: "Tanto non ci interessa, ma lasagna, ovviamente!",
    },
    {
      q: "Montagna o mare per la prossima vacanza?",
      a: "montagna",
      b: "mare",
      c: "Ok, me lo segno... poi vado dove mi pare!",
    },
    {
      q: "Film preferito: azione o commedia?",
      a: "azione",
      b: "commedia",
      c: "Bella domanda... Aspetta che cambio canale!",
    },
    {
      q: "Pizza margherita o capricciosa?",
      a: "margherita",
      b: "capricciosa",
      c: "Importante è che sia pizza, no?",
    },
    {
      q: "Per il caffè: zucchero o dolcificante?",
      a: "zucchero",
      b: "dolcificante",
      c: "Amaro, come la verità!",
    },
    {
      q: "Meglio leggere un libro o guardare una serie TV?",
      a: "libro",
      b: "serie TV",
      c: "Faccio una maratona... di sonno!",
    },
    {
      q: "Cosa scegli: palestra o divano?",
      a: "palestra",
      b: "divano",
      c: "Divano... E la palestra la guardo in foto!",
    },
    {
      q: "Preferisci viaggiare in treno o in auto?",
      a: "treno",
      b: "auto",
      c: "In realtà preferisco il teletrasporto!",
    },
    {
      q: "Birra o vino a cena?",
      a: "birra",
      b: "vino",
      c: "Dipende... chi paga?",
    },
    {
      q: "Meglio il gelato alla vaniglia o al cioccolato?",
      a: "vaniglia",
      b: "cioccolato",
      c: "Gelato d'inverno? Sei serio?",
    },
    {
      q: "Gatto o cane come animale domestico?",
      a: "gatto",
      b: "cane",
      c: "Un drago sarebbe troppo?",
    },
    {
      q: "Preferisci l'estate o l'inverno?",
      a: "estate",
      b: "inverno",
      c: "Preferisco il cambio di stagione, così mi lamento sempre!",
    },
    {
      q: "Meglio una vacanza avventurosa o rilassante?",
      a: "avventurosa",
      b: "rilassante",
      c: "Una rilassante avventura sul divano, grazie!",
    },
    {
      q: "Preferisci cucinare o ordinare cibo a domicilio?",
      a: "cucinare",
      b: "ordinare",
      c: "Ordino... e poi dico che l'ho cucinato io!",
    },
    {
      q: "Meglio fare shopping online o in negozio?",
      a: "online",
      b: "in negozio",
      c: "Shopping? Meglio risparmiare per il Capodanno!",
    },
    {
      q: "Concerto rock o serata jazz?",
      a: "rock",
      b: "jazz",
      c: "Una serata con la mia playlist è un'opzione?",
    },
    {
      q: "Cioccolata calda o caffè in inverno?",
      a: "cioccolata calda",
      b: "caffè",
      c: "Una scelta troppo difficile per una mente fredda!",
    },
    {
      q: "Preferisci leggere notizie online o su carta?",
      a: "online",
      b: "carta",
      c: "Notizie? Vivo nel mio mondo, grazie!",
    },
    {
      q: "Preferisci i film di supereroi o i thriller psicologici?",
      a: "supereroi",
      b: "thriller psicologici",
      c: "Dipende... Chi è il cattivo?",
    },
    {
      q: "Cosa scegli: videogiochi o giochi da tavolo?",
      a: "videogiochi",
      b: "giochi da tavolo",
      c: "Giochi? Solo se vinco sempre!",
    },
  ];
  let domanda = {};
  let loading = false;
  let showQuestion = true; // Control the display of questions and answers
  let timer = undefined

  onMount(() => {
    loadRandomQuestion();
  });

  function loadRandomQuestion() {
    domanda = domande[Math.floor(Math.random() * domande.length)];
    showQuestion = true; // Show the question again
  }

  async function handleAnswer() {
    if (loading) return;
    loading = true;
    showQuestion = false; // Hide the question to show the answer

    timer = setTimeout(() => {
      loading = false;
      loadRandomQuestion();
    }, 5000);
  }

    function handleNext() {
        loading = false;
        timer && clearTimeout(timer)
        loadRandomQuestion();
    }
</script>

<div class="flex flex-col justify-center items-center space-y-2 p-2">
  {#if domanda && domanda.q}
    <div class="max-w-md text-center space-y-2" class:fade={!showQuestion}>
      <h1 class="text-xl font-bold">{showQuestion ? domanda.q : domanda.c}</h1>
      {#if showQuestion}
        <div class="flex flex-col space-y-4 mt-6">
          <Button on:click={handleAnswer}>
            {domanda.a}
          </Button>
          <Button on:click={handleAnswer} variant="secondary">
            {domanda.b}
          </Button>
        </div>
      {/if}
    </div>
  {/if}
  {#if !showQuestion}
    <div class="fade-in">
      <Button on:click={handleNext}>Prossima Domanda</Button>
    </div>
  {/if}
</div>

<style>
  .fade {
    animation: fadeOut 5s forwards;
  }

  .fade-in {
    animation: fadeIn 0.3s forwards;
  }

  @keyframes fadeOut {
    0% {
      opacity: 1;
    }
    100% {
      opacity: 0;
    }
  }

  @keyframes fadeIn {
    0% {
      opacity: 0;
    }
    100% {
      opacity: 1;
    }
  }
</style>
