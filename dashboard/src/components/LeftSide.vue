<template>
  <div class="leftSide">
    <h5 class="mb-4 text-start mx-4 mt-3 fs-6">Dashboard</h5>
    <div class="d-flex">
      <img src="../assets/avatar.png" alt="avatar" />
      <div class="m-auto">
        <span>Welcome</span>
        <p class="fs-6"><strong>Mario Rossi</strong></p>
      </div>
    </div>
    <p class="font text-start mx-4 fw-bold">GENERAL</p>
    <hr />
    <div class="accordion open accordion-flush p-1" id="accordionFlushExample">
      <div class="accordion-item bg-item border-bottom-0">
        <h2 class="accordion-header" id="flush-headingOne">
          <button
            class="accordion-button collapsed bg-item"
            type="button"
            data-bs-toggle="collapse"
            data-bs-target="#flush-collapseOne"
            aria-expanded="false"
            aria-controls="flush-collapseOne"
          >
            <div class="d-flex" style="color: white">
              <i class="fa-solid fa-house-chimney"></i>
              <p class="mx-2">Home</p>
            </div>
          </button>
        </h2>
        <div
          id="flush-collapseOne"
          class="accordion-collapse collapse"
          aria-labelledby="flush-headingOne"
          data-bs-parent="#accordionFlushExample"
        >
          <ul class="accordion-body text-start mx-4">
            <li class="task-hover">
              <a href="#" style="color: white">Dashboard</a>
            </li>
            <li class="task-hover">
              <a href="#" style="color: white">Dashboard 2</a>
            </li>
            <li class="task-hover">
              <a href="#" style="color: white">Dashboard 3</a>
            </li>
          </ul>
        </div>
      </div>
      <div class="accordion-item bg-item border-bottom-0">
        <h2 class="accordion-header" id="flush-headingTwo">
          <button
            class="accordion-button collapsed bg-item dropdown-toggle-white"
            type="button"
            data-bs-toggle="collapse"
            data-bs-target="#flush-collapseTwo"
            aria-expanded="false"
            aria-controls="flush-collapseTwo"
          >
            <div class="d-flex" style="color: white">
              <i class="fa-solid fa-map-location"></i>
              <p class="mx-2">Maps</p>
            </div>
          </button>
        </h2>
        <div
          id="flush-collapseTwo"
          class="accordion-collapse collapse"
          aria-labelledby="flush-headingTwo"
          data-bs-parent="#accordionFlushExample"
        >
          <div class="accordion-body">
            Placeholder content for this accordion, which is intended to
            demonstrate the <code>.accordion-flush</code> class. This is the
            first item's accordion body.
          </div>
        </div>
      </div>
      <div class="accordion-item bg-item border-bottom-0">
        <h2 class="accordion-header" id="flush-headingThree">
          <button
            class="accordion-button collapsed bg-item"
            type="button"
            data-bs-toggle="collapse"
            data-bs-target="#flush-collapseThree"
            aria-expanded="false"
            aria-controls="flush-collapseThree"
          >
            <div class="d-flex" style="color: white">
              <i class="fa-solid fa-gear"></i>
              <p class="mx-2">Config</p>
            </div>
          </button>
        </h2>
        <div
          id="flush-collapseThree"
          class="accordion-collapse collapse"
          aria-labelledby="flush-headingThree"
          data-bs-parent="#accordionFlushExample"
        >
          <div class="accordion-body">
            Placeholder content for this accordion, which is intended to
            demonstrate the <code>.accordion-flush</code> class. This is the
            first item's accordion body.
          </div>
        </div>
      </div>
      <div class="accordion-item bg-item">
        <h2 class="accordion-header" id="flush-headingFour">
          <button
            class="accordion-button collapsed bg-item"
            type="button"
            data-bs-toggle="collapse"
            data-bs-target="#flush-collapseFour"
            aria-expanded="false"
            aria-controls="flush-collapseFour"
          >
            <div class="d-flex" style="color: white">
              <i class="fa-regular fa-envelope"></i>
              <p class="mx-2">Contacts</p>
            </div>
          </button>
        </h2>
        <div
          id="flush-collapseFour"
          class="accordion-collapse collapse"
          aria-labelledby="flush-headingFour"
          data-bs-parent="#accordionFlushExample"
        >
          <div class="accordion-body">
            Placeholder content for this accordion, which is intended to
            demonstrate the <code>.accordion-flush</code> class. This is the
            first item's accordion body.
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: "LeftSide",
  props: {
    first_name: String,
  },
};
</script>
<style scoped lang="scss">
img {
  width: 50px;
  height: 50px;
  border-radius: 50%;
  margin-bottom: 1.5rem;
  margin-left: 1.5rem;
}
.font {
  font-size: 10px;
}
ul {
  list-style-type: none;
}
.bg-item {
  background-color: #2b4154;
}
a {
  text-decoration: none;
}
.task-hover:hover {
  background-color: #354b60;
}
</style>
