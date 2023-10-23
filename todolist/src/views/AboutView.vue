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
        <button type="button" class="btn btn-primary" data-toggle="modal" data-target="#exampleModalCenter">Add new task</button>
      </div>
      <div class="modal fade" id="exampleModalCenter" tabindex="-1" role="dialog" aria-labelledby="exampleModalCenterTitle" aria-hidden="true">
      <div class="modal-dialog modal-dialog-centered" role="document">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title" id="exampleModalLongTitle">Add New Task </h5>
            <button type="button" class="close" data-dismiss="modal" aria-label="Close">
              <span aria-hidden="true">&times;</span>
            </button>
          </div>
          <div class="modal-body">
            <div class="modal-body">
              <div class="item">
                <label for="">Title</label>
                <input type="text" placeholder="e.g, study for the test" v-model="newTask.name" class="input_get">  
              </div>
              <div class="item">
                <label for="">Date</label>
                <input type="date" v-model="newTask.date" class="input_get">
              </div>
             <div class="item">
              <label for="">Desscription(optional)</label>
              <textarea name="" id="" cols="30" rows="6" v-model="newTask.description" class="input_get"></textarea>
             </div>
              <div class="item">
                <select name="" id="" v-model="newTask.dir" class="input_get">
                    <option value="">Main</option>
                </select>
              </div>
             <div class="item">
                <input type="radio" placeholder="Interval" v-model="newTask.interval" class="input_get">
                <span >Mark as important</span>
             </div>
              <div class="item">
                  <input type="radio" placeholder="Interval" v-model="newTask.important" class="input_get">
                  <span >Mark as completed</span>
              </div>
              
            </div>
          </div>
          <div class="modal-footer">
            <button type="button" class="btn btn-secondary" data-dismiss="modal">Close</button>
            <button type="button" class="btn btn-primary" @click="created()">Save changes</button>
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
  <div>
    <div class="grid-container">
      <div class="grid-item" v-for="item in todolist" :key="item.id">
        <div>
          <h5>{{ item.name }}</h5>
          <div class="des">
            {{ item.description }}
          </div>
          <div class="date">
            <span><i class="fa fa-calendar"></i></span> {{ item.date }}
          </div>
          <div class="row pt-2">
            <div class="col-lg-7">
              <button class="btn btn-danger">{{ item.interval }}</button>
            </div>
            <div class="col-lg-5 d-flex justify-space-between">
              <div class="row icon-task">
                <div class="col-lg-4"><i class="fa fa-star"></i></div>
                <div class="col-lg-4">
                  <i class="fa fa-trash" @click="deleteData(item.id)"></i>
                </div>
                <div class="col-lg-4"><i class="fa fa-ellipsis-v"></i></div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<style>
.input_get{
  width: 100%;
  padding: 10px;
  border-radius: 10px;
}
.about {
  margin: 20px 0px;
  display: flex;
  justify-content: space-between;
}
.icon-task {
  font-size: 25px;
}
.grid-container {
  display: grid;
  grid-template-columns: auto auto auto;
  padding: 10px;
}
.grid-item {
  background-color: #7c3aed;
  border: 1px solid rgba(0, 0, 0, 0.8);
  padding: 20px;
  border-radius: 10px;
  margin: 10px;
}
.date {
  padding: 10px 10px 25px 5px;
  border-bottom: 3px dashed darkgray;
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
.togger {
  display: flex;
  justify-content: space-between;
}
.text-togger {
  padding: 10px;
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
  margin: 30px 0px;
  padding: 15px;
  border-radius: 5px;
  border: none;
  background: #f1f5f9;
}
</style>
<script>
export default {
  data() {
    return {
      todolist: [],
      newTask: {
      name: '',
      description: '',
      date: '',
      interval: '',
      dir: '',
      important:'',
    },
    };
  },
  methods: {
    async getData() {
      try {
        const response = await fetch(
          "https://64d20150f8d60b174361428e.mockapi.io/todolist"
        );
        const data = await response.json();
        this.todolist = data;
      } catch (error) {
        console.error("Error fetching data:", error);
      }
    },
    async deleteData(id) {
      try {
        const response = await fetch(
          `https://64d20150f8d60b174361428e.mockapi.io/todolist/${id}`,
          { method: 'DELETE' }
        );
        
        if (response.ok) {
          this.getData(); 
          console.log('ok');
        } else {
          console.error('Xoa k thanh cong');
        }
      } catch (error) {
        console.error("loiiiiii roiiii:", error);
      }
    },
    async created() {
      try {
        const response = await fetch(`https://64d20150f8d60b174361428e.mockapi.io/todolist`, {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json',
          },
          body: JSON.stringify({
            name: this.newTask.name,
            description: this.newTask.description,
            date: this.newTask.date,
            interval: this.newTask.interval,
          }),
        });

        if (response.ok) {
          const newData = await response.json();
          this.todolist.push(newData);
          $('#exampleModalCenter').modal('hide'); 
          this.newTask = {
            name: '',
            description: '',
            date: '',
            interval: '',
            dir: '',
            important:'',
          };
        } else {
          console.error('Failed to create task');
        }
      } catch (error) {
        console.error('Error creating task:', error);
      }
    }
  },
  mounted() {
    this.getData();
    this.deleteData();
  },
};
</script>
