<template>
  <div>
    <div class="title">
      <div class="content">
        <div class="line"></div>
        <h1>Donnez votre avis</h1>
        <div class="line"></div>
      </div>

      <img src="/images/logo-arrows.png"/>
    </div>

    <Steps :currentStep.sync="currentStep" class="steps">
      <Step image="Group.svg">
        <form @submit.prevent="currentStep++">
          <div class="firstname-group">
            <InputItem
              id="firstname"
              label="Prénom *"
              v-model="payload.firstname"
              placeholder="Tedi.Ber"
            />

            <DateItem
              id="birthdate"
              label="Date de naissance *"
              v-model="payload.birthdate"
            />
          </div>

          <InputItem
            id="email"
            type="email"
            label="Email *"
            description="(non divulgué - uniquement utilisé pour relier cet avis à votre commande)"
            v-model="payload.email"
            placeholder="tedi.Ber@tediber.fr"
          />

          <InputItem
            id="city"
            label="Ville *"
            v-model="payload.city"
            placeholder="Paris"
          />

          <div class="submit-wrapper">
            <button type="submit">Étape suivante</button>
          </div>
        </form>
      </Step>

      <Step image="Fichier 29-100.svg">
        <form @submit.prevent="currentStep++">
          <RadioGroupItem
            label="Dans quelle position dormez-vous ? *"
            :list="positionList"
            v-model="payload.position"
          />

          <RadioGroupItem
            label="Qui dort sur le matelas ? *"
            :list="whoList"
            v-model="payload.who"
          />

          <StarsItem
            label="Évaluation du matelas *"
            v-model="payload.mattressNote"
          />

          <CheckboxGroupItem
            label="Étiez-vous concerné(e) par un ou plusieurs de ces problèmes avant ?"
            :list="problemsList"
            v-model="payload.problems"
          />

          <TextareaItem
            id="experience"
            label="Quelques mots au sujet du matelas Tediber *"
            v-model="payload.mattressComment"
            :placeholder="`Décrivez votre expérience avec votre nouveau produit Tediber ?
Qu'est-ce qui vous plait le plus ?
Pourquoi le recommanderiez-vous ?`"
          />

          <div class="submit-wrapper">
            <button type="submit">Étape suivante</button>
          </div>
        </form>
      </Step>

      <Step image="pillow.png">
        <form @submit.prevent="send">
          <StarsItem
            label="Évaluation de l'oreiller *"
            v-model="payload.pillowNote"
          />

          <TextareaItem
            id="experience"
            label="Quelques mots au sujet de l'oreiller Tediber *"
            v-model="payload.pillowComment"
            :placeholder="`Décrivez votre expérience avec votre nouveau produit Tediber ?
Qu'est-ce qui vous plait le plus ?
Pourquoi le recommanderiez-vous ?`"
          />

          <div class="submit-wrapper">
            <button type="submit">Envoyer</button>
          </div>
        </form>
      </Step>
    </Steps>

    <div class="payload" v-html="payloadHtml"></div>
  </div>
</template>

<script>
import Steps from './Steps';
import Step from './Step';
import InputItem from './InputItem';
import DateItem from './DateItem';
import RadioGroupItem from './RadioGroupItem';
import CheckboxGroupItem from './CheckboxGroupItem';
import TextareaItem from './TextareaItem';
import StarsItem from './StarsItem';

export default {
  components: {
    StarsItem,
    TextareaItem,
    CheckboxGroupItem,
    RadioGroupItem,
    DateItem,
    InputItem,
    Step,
    Steps,
  },
  data() {
    return {
      currentStep: 0,
      payload: {
        firstname: '',
        birthdate: '',
        email: '',
        city: '',
        who: '',
        position: '',
        problems: [],
        mattressNote: 0,
        mattressComment: '',
        pillowNote: 0,
        pillowComment: '',
      },
    };
  },
  computed: {
    positionList() {
      return [
        { name: 'position', image: 'Sur le dos', text: 'sur le dos', value: 'sur le dos' },
        { name: 'position', image: 'Sur le ventre', text: 'sur le ventre', value: 'sur le ventre' },
        { name: 'position', image: 'Sur le côté', text: 'sur le côté', value: 'sur le côté' },
        { name: 'position', image: 'étoile', text: 'en étoile', value: 'en étoile' },
      ];
    },
    whoList() {
      return [
        { name: 'who', image: 'un', text: 'un', value: 'un' },
        { name: 'who', image: 'Deux', text: 'deux', value: 'deux' },
        { name: 'who', image: 'autre', text: 'autre', value: 'autre' },
      ];
    },
    problemsList() {
      return [
        { value: 'mal de dos au réveil', label: 'mal de dos au réveil' },
        { value: 'trop chaud / froid la nuit', label: 'trop chaud / froid la nuit' },
        { value: 'jambes lourdes au réveil', label: 'jambes lourdes au réveil' },
        { value: 'quand l\'autre bougeait cela me réveillait', label: 'quand l\'autre bougeait cela me réveillait' },
        { value: 'réveil difficile', label: 'réveil difficile' },
      ];
    },
    payloadHtml() {
      return JSON.stringify(this.payload, null, 2).replace(/ /g, '&nbsp;').replace(/\n/g, '<br />');
    },
  },
  methods: {
    send() {
      alert('send payload');
    },
  },
};
</script>

<style lang="scss" scoped>
.title {
  margin-bottom: 48px;

  .content {
    display: flex;
    align-items: center;
    margin-bottom: 16px;

    .line {
      border-bottom: 1px solid #555;
      width: 100%;
    }

    h1 {
      text-transform: uppercase;
      white-space: nowrap;
      padding: 0 32px;
      letter-spacing: 2px;
      font-weight: normal;
      font-size: 20px;
    }
  }

  img {
    display: block;
    margin: auto;
    height: 20px;
  }
}

.steps {
  max-width: 800px;
  margin: auto;
}

.firstname-group {
  margin-bottom: 24px;

  @media (min-width: 768px) {
    margin-bottom: 0;
    display: flex;
    width: 100%;

    > * {
      width: 100%;

      &:last-child {
        margin-left: 16px;
      }
    }
  }
}

.payload {
  font-family: monospace;
  padding: 16px;
  background: #eee;
  margin: 60px 0;
}

.submit-wrapper {
  display: flex;
  justify-content: flex-end;

  button {
    background: orange;
    color: #fff;
    border: none;
    padding: 16px;
    font-size: 16px;
    font-weight: bold;
    letter-spacing: 3px;
    text-transform: uppercase;
    cursor: pointer;
  }
}
</style>
