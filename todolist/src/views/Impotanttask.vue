<template>
  <div class="about">
    <div class="buttonsearch">
      <input type="search" placeholder="Search task" />
      <div class="text">
        <img src="../assets/seach.png" alt="" width="18px" />
      </div>
    </div>
    <h4 class="text-day">2023,jul 31</h4>
    <div class="togger">
      <div class="text-togger">
        <img
          src="../assets/notification.png"
          alt=""
          width="18px"
          height="20px"
        />
      </div>
      <div class="icon-togger">
        <!-- Button trigger modal -->
        <button
          type="button"
          class="btn btn-primary"
          data-bs-toggle="modal"
          data-bs-target="#exampleModal"
        >
          Add new task
        </button>

        <!-- Modal -->
        <div
          class="modal fade"
          id="exampleModal"
          tabindex="-1"
          aria-labelledby="exampleModalLabel"
          aria-hidden="true"
        >
          <div class="modal-dialog">
            <div class="modal-content">
              <div class="modal-header">
                <h5 class="modal-title" id="exampleModalLabel">Add a task</h5>
                <button
                  type="button"
                  class="btn-close"
                  data-bs-dismiss="modal"
                  aria-label="Close"
                ></button>
              </div>
              <div class="modal-body">
                <form @submit.prevent="submit">
                  <label for="">Title</label>
                  <input
                    type="text"
                    name=""
                    id=""
                    placeholder="e.g,study for test"
                    class="input-type"
                    v-model="form.text"
                  />
                  <label for="">Date</label>
                  <input
                    type="date"
                    name="date"
                    id=""
                    class="input-type"
                    v-model="form.date"
                  />
                  <label for="">Description</label>
                  <textarea
                    name=""
                    id=""
                    cols="30"
                    rows="10"
                    placeholder="e.g,study for the test"
                    class="input-type"
                    v-model="form.description"
                  ></textarea>
                  <label for="">Select a directory</label>
                  <select name="" id="" class="input-type" v-model="form.city">
                    <option value="Main">Main</option>
                  </select>
                  <input
                    type="radio"
                    name=""
                    id=""
                    class=""
                    value="Completed"
                    v-model="form.interval"
                  />
                  <label for="">Mark as Completed</label>
                  <br />
                  <input
                    type="radio"
                    name=""
                    id=""
                    class=""
                    value="Uncompleted"
                    v-model="form.interval"
                  />
                  <label for="">Mark as Important</label>
                  <div class="modal-footer">
                    <button
                      type="button"
                      class="btn btn-secondary"
                      data-bs-dismiss="modal"
                    >
                      Close
                    </button>
                    <button type="submit" class="btn btn-primary">Add</button>
                  </div>
                </form>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
  <div class="item">
    <p>Today's tasks (0 tasks)</p>
  </div>
  <div class="icon-menu">
    <div class="item-icon">
      <img src="../assets/list.png" alt="" width="25px" height="25px" />
      <img src="../assets/sizebar.png" alt="" width="25px" height="25px" />
    </div>
    <div class="select-option">
      <select name="cars" id="cars">
        <option value="Sort by">Sort by</option>
        <option value="Order added">Order added</option>
        <option value="Earlier first">Earlier first</option>
        <option value="Later first">Later first</option>
        <option value="Completed first">Completed first</option>
        <option value="Uncompleted first">Uncompleted first</option>
      </select>
    </div>
  </div>
  <div class="row">
    <div class="col-lg-4">
      <div v-if="submittedDataArray.length > 0" class="submitted-data">
        <div v-for="(data, index) in submittedDataArray" :key="index">
          <div class="row">
            <div class="col-lg-8"></div>
            <div class="col-lg-3">
              <div class="main">
                <p>{{ data.city }}</p>
              </div>
            </div>
          </div>
          <div class="item-task">
            <strong>Name: {{ data.text }}</strong>
            <p class="description">{{ data.description }}</p>
            <p class="pt-5 pb-5 date">
              <span><i class="fa fa-calendar"></i></span> {{ data.date }}
            </p>
            <div class="row pt-2">
              <div class="col-lg-7">
                <button class="btn btn-danger">{{ data.interval }}</button>
              </div>
              <div class="col-lg-5 d-flex justify-space-between">
                <div class="row icon-task">
                  <div class="col-lg-4"><i class="fa fa-star"></i></div>
                  <div class="col-lg-4" @click="deleteTask(index)">
                    <i class="fa fa-trash"></i>
                  </div>
                  <div class="col-lg-4"><i class="fa fa-ellipsis-v"></i></div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      form: {
        text: "",
        description: "",
        city: "",
        interval: "",
        date: "",
      },
      submittedDataArray: [],
    };
  },
  methods: {
    async submit() {
      this.submittedDataArray.push({ ...this.form });
      this.form = {
        text: "",
        description: "",
        city: "",
        interval: "",
        date: "",
      };
      this.isFormOpen = true;
    },
    deleteTask(index) {
      this.submittedDataArray.splice(index, 1);
    },
  },
};
</script>
<style>
.icon-task {
  font-size: 25px;
}
.date {
  border-bottom: 2px dashed darkgray;
}
.main p {
  text-align: center;
  padding-top: 5px;
  color: red;
}
.main {
  padding: 3px;
  background-color: rgb(234, 159, 183);
  border-top-left-radius: 5px;
  border-top-right-radius: 5px;
}
.item {
  font-size: 22px;
  padding-top: 40px;
  font-weight: bold;
}
.about {
  padding-top: 10px;
  width: 100%;
  display: flex;
  justify-content: space-between;
}
.add {
  padding: 15px;
  border-radius: 5px;
  background: #7c3aed;
  border: none;
  width: 100%;
  color: #fff;
}
.togger {
  display: flex;
  justify-content: space-between;
}
.text-togger {
  padding: 10px;
}
.buttonsearch {
  position: relative;
}
.buttonsearch input {
  width: 100%;
  padding: 15px;
  border-radius: 5px;
  border: none;
  background-color: #f1f5f9;
}
.text {
  position: absolute;
  top: 15px;
  left: 180px;
}

.text-day {
  padding-top: 10px;
}
.item-icon {
  display: flex;
  justify-content: space-between;
  width: 5%;
  padding-top: 30px;
  margin: 5px;
}
.icon-menu {
  display: flex;
}
.select-option {
  width: 95%;
  text-align: right;
}
.select-option select {
  width: 180px;
  margin-top: 30px;
  padding: 15px;
  border-radius: 5px;
  border: none;
  background: #f1f5f9;
}
.input-type {
  width: 100%;
  padding: 8px;
  border-radius: 7px;
  margin: 5px;
}
.item-task {
  color: #f1f5f9;
  background: #7c3aed;
  border-radius: 15px;
  padding: 15px;
}
</style>
