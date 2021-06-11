<template>
  <div>
    <section class="bg-top">
    </section>
    <section class="bg-pattern d-md-none">
      <div class="container my-4">
        <h2>Is the web possible without the spider?</h2>
        <p>
          Are space and time physical objects that would continue to exist even it living creatures were removed from the scene?
        </p>
        <p>
          Figuring out the nature of the real world has obsessed scientists and philosophers for millennia.
          Three hundred years ago, the Irish empiricist prescient observation: The only thing we can perceive are our perceptions.
        </p>
      </div>
    </section>
    <section class="container auction text-center my-4">
      <h5>
        Viimati lõppenud
      </h5>
      <div class="row">
        <div class="col-12 col-md-4">
          <img
            v-if="auction.imageUrl"
            :src="auction.imageUrl"
          >
        </div>
        <div class="col-12 col-md-8 mt-md-5">
          <h3 class="my-4">
            {{ auction.title }}
          </h3>
          <div class="row">
            <div class="col">
              <div class="orange h3">
                {{ auction.currentPriceEur }}€
              </div>
              <small>
                hetke hind
              </small>
            </div>
            <div class="col">
              <div class="orange h4">
                {{ timeLeftLabel }}
              </div>
              <small>
                lõpuni jäänud
              </small>
            </div>
            <div class="col">
              <div class="orange h4">
                {{ auction.currentBids }}
              </div>
              <small>
                pakkumist
              </small>
            </div>
          </div>
        </div>
      </div>
    </section>
    <section class="bg-mid text-white">
      <div class="container my-5">
        <h2>Messing with the light</h2>
        <div class="row">
          <div class="col-12 col-md-6">
            <ul>
              <li>
                Quantum mechanics is the physicist's most accurate model for describing the world of the atom.
              </li>
              <li>
                But it also makes some of the most persuasive arguments that conscious perception is integral to the workings of the universe.
              </li>
              <li>
                Quantum theory tells us that an unobserved small object.
              </li>
            </ul>
          </div>
          <div class="col-12 col-md-6 mt-5 mt-md-0">
            <h4>What accomplishes this collapse?</h4>
            <p>
              What accomplishes this collapse? Messing with it. Hitting it with a bit of light in order to take its picture. Just looking at it does the job.
            </p>
            <p>
              Experiments suggest mere knowledge in the experimenter's mind is sufficient to collapse a wave function and convert possibility to reality.
            </p>
          </div>
        </div>
      </div>
    </section>
    <section class="bg-pattern">
      <div class="container mt-5">
        <h2>Want higher?</h2>
        <p>
          Before these experiments most physicists believed in an objective, independent universe.
          They still clung to the assumption that physical states exist in some absolute sense before they are measured.
        </p>
      </div>
    </section>
    <section class="bg-pattern">
      <div class="container my-5">
        <div class="row">
          <div class="col-12 col-md-6">
            <h2>Contact us</h2>
            <p>Before these experiments most</p>
            <p>
              <i class="icon email"></i>
              <span class="icon-text">
                info@allepal.ee
              </span>
              <br>
              <i class="icon phone"></i>
              <span class="icon-text">
                +372 65656565
              </span>
            </p>
          </div>
          <div class="col-12 col-md-6">
            <h2>Location</h2>
            <p>
              AllePal OÜ<br>
              Maakri 23a<br>
              10145 Tallinn, Eesti
            </p>
          </div>
        </div>
      </div>
    </section>
    <section class="p-0">
      <div class="map-responsive">
        <iframe src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d2029.0428264019786!2d24.758314916501337!3d59.43236028169496!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x469294a0841313f9%3A0x355dccd90b569857!2sMaakri%2023a%2C%2010145%20Tallinn!5e0!3m2!1sen!2see!4v1623329884265!5m2!1sen!2see" style="border:0;" allowfullscreen="" loading="lazy"></iframe>
      </div>
    </section>
  </div>
</template>

<script>
import axios from 'axios'

const MILLISECONDS_MINUTE = 60 * 1000;
const MILLISECONDS_HOUR = 60 * MILLISECONDS_MINUTE;
const MILLISECONDS_DAY = 24 * MILLISECONDS_HOUR;

export default {
  name: 'Moon',
  data () {
    return {
      auction: {
        currentPriceEur: 0,
        currentBids: 0
      },
      timeToEnd: 0
    }
  },
  computed: {
    timeLeft () {
      return {
        days: Math.floor(this.timeToEnd / MILLISECONDS_DAY),
        hours: Math.floor((this.timeToEnd % MILLISECONDS_DAY) / MILLISECONDS_HOUR),
        minutes: Math.floor((this.timeToEnd % MILLISECONDS_HOUR) / MILLISECONDS_MINUTE),
        seconds: Math.floor((this.timeToEnd % MILLISECONDS_MINUTE) / 1000)
      }
    },
    timeLeftLabel () {
      if (this.timeToEnd === 0) {
        return 'Okjson on lõppenud'
      }

      const labels = []
      const timeLeft = this.timeLeft

      if (timeLeft.days > 0) {
        labels.push(timeLeft.days + ' päeva')
      }

      if (timeLeft.hours > 0) {
        labels.push(timeLeft.hours + ' tundi')
      }

      if (timeLeft.minutes > 0 && labels.length < 2) {
        labels.push(timeLeft.minutes + ' minutit')
      }

      if (timeLeft.seconds > 0 && labels.length < 2) {
        labels.push(timeLeft.seconds + ' sekundit')
      }

      return labels.join(', ')
    }
  },
  async created () {
    axios.get(`https://api.osta.ee/api/items/active/${process.env.VUE_APP_AUCTION_ID}`)
      .then(auctionResponse => {
        if (auctionResponse && auctionResponse.data) {
          this.auction = auctionResponse.data
          this.setTimeToEnd()
        }
      }, () => {})
  },
  methods: {
    setTimeToEnd () {
      if (this.auction.dateEnd) {
        const endDate = new Date(this.auction.dateEnd)
        this.timeToEnd = endDate.getTime() - Date.now()

        if (this.timeToEnd <= 0) {
          this.timeToEnd = 0
          return;
        }

        setTimeout(this.setTimeToEnd, 1000)
      }
    }
  }
}
</script>

<style lang="scss">
@import "~bootstrap/scss/mixins/breakpoints";
@import "~bootstrap/scss/functions";
@import "~bootstrap/scss/variables";

.bg-top {
  height: 283px;
  background: url('~@/assets/images/mobile-top.png') no-repeat center center;

  @include media-breakpoint-up(md) {
    height: 800px;
    background: #000 url('~@/assets/images/top.png') no-repeat center center;
  }
}

.bg-mid {
  background: url('~@/assets/images/mobile-mid.png') no-repeat center center;
  background-size: cover;

  @include media-breakpoint-up(md) {
    background: url('~@/assets/images/middle.png') no-repeat center center;
  }
}

.bg-pattern {
  background: url('~@/assets/images/pattern.png');
}

.icon {
  display: inline-block;
  height: 30px;
  width: 30px;
  background-repeat: no-repeat;
  background-position: center center;

  &.email {
    background-image: url('~@/assets/images/envelope.png');
  }

  &.phone {
    background-image: url('~@/assets/images/phone.png');
  }
}

.icon-text {
  position: relative;
  top: -10px;
  left: 5px;
}

h2, h4 {
  text-transform: uppercase;
  font-family: Oswald,serif;
}

section {
  padding: 4px;

  p {
    margin: 1rem 0;
  }
}

section.auction {
  h5 {
    color: #999;
  }

  img {
    max-width: 100%;
    max-height: 100%;
    padding: 10px;
  }

  .orange {
    color: #fb6520;
    font-weight: bold;
  }
}

ul {
  li {
    margin: 1rem 0;
  }
}

.map-responsive {
  position: relative;
  height: 500px;

  iframe {
    height: 100%;
    width: 100%;
  }
}
</style>
