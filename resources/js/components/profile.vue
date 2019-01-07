<style>
    .widget-user-header{
        background-position: center center;
        background-size: cover;
    }
    
    .widget-user-image{
        margin-top: 200px;
    }
</style>

<template>
    <div class="container">
        <div class="row">
            <div class="col-md-12 mt-3">
                <div class="card card-widget widget-user">
                    <!-- Add the bg color to the header using any of the bg-* classes -->
                    <div class="widget-user-header text-white" style="background-image: url('./img/cover.jpg');height: 300px;">
                        <h3 class="widget-user-username">{{this.form.name}}</h3>
                        <h5 class="widget-user-desc">{{this.form.type}}</h5>
                    </div>
                    <div class="widget-user-image">
                        <img class="img-circle" :src="getProfilePhoto()" alt="User Avatar">
                    </div>
                    <div class="card-footer">
                        <div class="row">
                            <div class="col-sm-4 border-right">
                                <div class="description-block">
                                    <h5 class="description-header">3,200</h5>
                                    <span class="description-text">SALES</span>
                                </div>
                                <!-- /.description-block -->
                            </div>
                            <!-- /.col -->
                            <div class="col-sm-4 border-right">
                                <div class="description-block">
                                    <h5 class="description-header">13,000</h5>
                                    <span class="description-text">FOLLOWERS</span>
                                </div>
                                <!-- /.description-block -->
                            </div>
                            <!-- /.col -->
                            <div class="col-sm-4">
                                <div class="description-block">
                                    <h5 class="description-header">35</h5>
                                    <span class="description-text">PRODUCTS</span>
                                </div>
                                <!-- /.description-block -->
                            </div>
                            <!-- /.col -->
                        </div>
                        <!-- /.row -->
                    </div>
                </div>
            </div>
    
            <div class="col-md-12 mr-20">
                <div class="card">
                    <div class="card-header p-2">
                        <ul class="nav nav-pills">
                            <li class="nav-item"><a class="nav-link" href="#activity" data-toggle="tab">Activity</a></li>
                            <li class="nav-item"><a class="nav-link active show" href="#settings" data-toggle="tab">Settings</a></li>
                        </ul>
                    </div><!-- /.card-header -->
                    <div class="card-body">
                        <div class="tab-content">
                            <div class="tab-pane" id="activity">
                                <!-- Post -->
                                <div class="post">
                                    <h3 class="text-center">display user activity</h3>
                                </div>
                                <!-- /.post -->
                            </div>
                            <!-- /.tab-pane -->
                    
                            <div class="tab-pane active show" id="settings">
                                <form class="form-horizontal">
                                    <div class="form-group">
                                        <label for="inputName" class="col-sm-2 control-label">Name</label>
                                
                                        <div class="col-sm-10">
                                            <input  v-model="form.name" type="email"
                                                    class="form-control" id="inputName" placeholder="Name"
                                                    :class="{ 'is-invalid': form.errors.has('name') }">
                                            <has-error :form="form" field="name"></has-error>
                                        </div>
                                    </div>
                                    <div class="form-group">
                                        <label for="inputEmail" class="col-sm-2 control-label">Email</label>
                                
                                        <div class="col-sm-10">
                                            <input  v-model="form.email"
                                                    type="email" class="form-control" id="inputEmail" placeholder="Email"
                                                    :class="{ 'is-invalid': form.errors.has('email') }">
                                            <has-error :form="form" field="email"></has-error>
                                        </div>
                                    </div>
                                    <div class="form-group">
                                        <label for="inputbio" class="col-sm-2 control-label">Bio</label>
                                
                                        <div class="col-sm-10">
                                            <textarea v-model="form.bio" type="text" id="inputbio" name="bio" placeholder="bio"
                                                      class="form-control" :class="{ 'is-invalid': form.errors.has('bio') }"></textarea>
                                            <has-error :form="form" field="bio"></has-error>
                                        </div>
                                    </div>
                                    <div class="form-group">
                                        <label for="inputType" class="col-sm-2 control-label">Type</label>
                                
                                        <div class="col-sm-10">
                                            <select v-model="form.type" name="type" id="inputType" class="form-control">
                                                <option value="">Select user role</option>
                                                <option value="admin">Admin</option>
                                                <option value="user">Standerd User</option>
                                                <option value="author">Author</option>
                                            </select>
                                        </div>
                                    </div>
                                    <div class="form-group">
                                        <label for="inputPassword" class="col-sm-2 control-label">Password</label>
                                
                                        <div class="col-sm-10">
                                            <input  v-model="form.password"
                                                    type="password" class="form-control" id="inputPassword" placeholder="Password"
                                                    :class="{ 'is-invalid': form.errors.has('password') }">
                                            <has-error :form="form" field="password"></has-error>
                                        </div>
                                    </div>
                                    <div class="form-group">
                                        <div class="col-sm-offset-2 col-sm-10">
                                            <div class="checkbox">
                                                <label>
                                                    <input type="file" @change="updateProfile" name="photo">
                                                </label>
                                            </div>
                                        </div>
                                    </div>
                                    <div class="form-group">
                                        <div class="col-sm-offset-2 col-sm-10">
                                            <button @click.prevent="updateInfo" type="submit" class="btn btn-danger">Update</button>
                                        </div>
                                    </div>
                                </form>
                            </div>
                            <!-- /.tab-pane -->
                        </div>
                        <!-- /.tab-content -->
                    </div><!-- /.card-body -->
                </div>
                <!-- /.nav-tabs-custom -->
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        data(){
            return{
                form: new Form({
                    id: '',
                    name: '',
                    email: '',
                    password: '',
                    type: '',
                    bio: '',
                    photo: ''
                })
            }
        },
        
        mounted() {
            console.log('Component mounted.')
        },
        
        methods: {
            
            getProfilePhoto(){
                let photo = (this.form.photo.length > 200) ? this.form.photo : "img/profile/"+ this.form.photo ;
                return photo;
            },
            
            updateInfo(){
                this.$Progress.start();
                this.form.put('api/profile/')
                    .then(()=>{
    
                        Fire.$emit('AfterCreate');
                        
                        this.$Progress.finish();
                    })
                    .catch(()=>{
                        this.$Progress.fail();
                    });
            },
            
          updateProfile(e){
              // console.log('uploading');
              let file = e.target.files[0];
              console.log(file);
              let reader = new FileReader();
              if (file['size'] < 2111775) {
                  reader.onloadend = (file) => {
                      // console.log('RESULT', reader.result);
                      this.form.photo = reader.result;
                  }
                  reader.readAsDataURL(file);
              }else {
                  swal({
                      type: 'error',
                      title: 'Oops',
                      text: 'Ypu are uploading a large file',
                  })
              }
          }
        },
        
        created() {
            axios.get('api/profile')
                .then(({data}) => (this.form.fill(data)));
        }
    }
</script>
