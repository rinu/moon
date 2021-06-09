<template>
  <div>
    <section class="bg-top">
    </section>
    <section class="bg-pattern">
      <h2>Is the web possible without the spider?</h2>
      <p>
        Are space and time physical objects that would continue to exist even it living creatures were removed from the scene?
      </p>
      <p>
        Figuring out the nature of the real world has obsessed scientists and philosophers for millennia.
      </p>
    </section>
    <section>
      Viimati lõppenud
    </section>
    <section class="bg-mid text-white">
      <h2>Messing with the light</h2>
      <ul>
        <li>
          Quantum
        </li>
        <li>
          But it also
        </li>
        <li>
          Quantum
        </li>
      </ul>
      <h3>What accomplishes this collapse?</h3>
      <p>
        What accomplishes this collapse?
      </p>
      <p>
        Experiments suggest mere knowledge
      </p>
    </section>
    <section class="bg-pattern">
      <h2>Want higher?</h2>
      <p>
        Before these experiments most physicists believed in an objective, independent universe.
      </p>
    </section>
    <section class="bg-pattern">
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
    </section>
    <section class="bg-pattern">
      <h2>Location</h2>
      <p>
        AllePal OÜ<br>
        Maakri 23a<br>
        10145 Tallinn, Eesti
      </p>
    </section>
    <section>
      map
    </section>
  </div>
</template>

<script>
export default {
  name: 'Moon'
}
</script>

<style lang="scss">
.bg-top {
  height: 283px;
  background: url('~@/assets/images/mobile-top.png') no-repeat center center;
}

.bg-mid {
  background: url('~@/assets/images/mobile-mid.png');
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

h2 {
  text-transform: uppercase;
}

section {
  padding: 10px;

  p {
    margin: 0;
    padding: 5px 0;
  }
}
</style>
