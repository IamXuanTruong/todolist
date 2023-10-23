<template>
  <div class="menu">
    <div>
      <p class="text-header">To-Do-List</p>
    </div>
    <div class="button">
      <button
        type="button"
        class="btn btn-primary"
        data-bs-toggle="modal"
        data-bs-target="#exampleModal"
      >
        Add new task
      </button>
    </div>
    <div id="formContainer" v-show="isShow">
      <form id="form">
        <input type="text" name="taskName" placeholder="Tên công việc" />
        <input type="submit" value="Gửi" />
      </form>
    </div>

    <div class="select-menu">
      <ul>
        <li><RouterLink to="/today">Today's tasks</RouterLink></li>
        <li><RouterLink to="/">All tasks</RouterLink></li>
        <li><RouterLink to="/impotant">Important tasks</RouterLink></li>
        <li><RouterLink to="/completed">Completed tasks</RouterLink></li>
        <li><RouterLink to="/uncompleted">Uncompleted tasks</RouterLink></li>
        <div class="dropdown">
          <button
            class="mt-3 btn btn-outline-dark dropdown-toggle"
            type="button"
            id="dropdownMenuButton1"
            data-bs-toggle="dropdown"
            aria-expanded="false"
          >
            Directories
          </button>

          <ul class="dropdown-menu" aria-labelledby="dropdownMenuButton1">
            <li><a class="dropdown-item drop-text" href="#">Main</a></li>
            <li>
              <a
                class="dropdown-item drop-button"
                href="#"
                type="button"
                data-bs-toggle="modal"
                data-bs-target="#exampleModal"
                >New <span><i class="fa fa-plus-square"></i></span
              ></a>
            </li>
          </ul>
        </div>
      </ul>
    </div>
  </div>
</template>

<style scoped>
.drop-button {
  border: 2px dashed rgba(0, 0, 0, 0.3);
  margin: 0px 10px;
}
.drop-text {
  margin: 0px 10px;
}
.menu {
  margin-right: 10px;
  border-right: 2px solid rgba(0, 0, 0, 0.3);
  height: 1000px;
}
h1 {
  font-weight: 500;
  font-size: 2.6rem;
  position: relative;
  top: -10px;
}
.add {
  margin: 0 auto;
  border-radius: 5px;
  background: #7c3aed;
  border: none;
  width: 90%;
  color: #fff;
}
.text-header {
  padding: 10px;
  text-align: center;
  font-size: 30px;
  font-weight: bold;
  font-family: "Lucida Sans", "Lucida Sans Regular", "Lucida Grande",
    "Lucida Sans Unicode", Geneva, Verdana, sans-serif;
}
.button {
  width: 80%;
  margin: 0 auto;
}
.button button {
  width: 100%;
  padding: 10px;
}
.select-menu ul li {
  text-align: left;
  padding: 20px 20px 20px 0px;
  list-style-type: none;
}
.select-menu ul li:hover a {
  color: red;
}
.select-menu ul li a {
  text-decoration: none;
  color: black;
}
</style>

<script>
export default {
  components: {},
  props: {},
  data() {
    return {
      isShow: false,
    };
  },
  created() {},
  methods: {
    formSubmit() {
      this.isShow = true;
    },
  },
  mounted() {},
};
</script>
