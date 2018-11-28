# js-extend--copy-
js 模拟类 父与子的继承复制

                显示混入
                  var Vehicle={
                    sefg:3,
                    ignition:function(){
                       console.log("我是父类的ignition方法")
                    },
                    drive:function(){
                       console.log(this) //{bera: 90, drive: ƒ, sefg: 3, ignition: ƒ}
                       this.ignition()
                       console.log("我是父类drive方法")
                    }
                 }         

                function mixin(n1,n2){
                 for(var key in n1){
                   if(!(key in n2)){
                      n2[key]=n1[key]
                     }
                    }
                   return n2
                  }


               var Cat=mixin(Vehicle,{
                       bera:90,
                       drive:function(){
                        Vehicle.drive.call(this);
                       console.log("我是子类drive方法")
                     }
               })

               Cat.drive()    //我是父类的ignition方法
                              //我是父类drive方法
                              //我是子类drive方法

        上面这种继承模式不解？可看下面代码
        
        
                 var Cat=mixin(Vehicle,{
                   bera:90,
                   get:function(){
                     this.drive() 
                   }   
               })
            console.log(Cat) //{bera: 90, get: ƒ, sefg: 3, ignition: ƒ, drive: ƒ}
            Cat.get() //我是父类的ignition方法
                      //我是父类drive方法  
        
        
        
   寄生继承
   
    
               function Vehicle(){
                   this.engines=3;
              }
              Vehicle.prototype.ignition=function(){
                  console.log("我是ignition方法")         
              }
             Vehicle.prototype.drive=function(){
                this.ignition()
                console.log("我是drive方法")
                console.log(this) //Vehicle {engines: 3, drive: ƒ}
             }
              function Cat(){
                  var cat=new Vehicle()
                  var vuhDrive=cat.drive;
                   cat.drive=function(){
                    vuhDrive.call(this);
                   }
                  return cat;
              }
             var cat=new Cat();
              cat.drive()   //我是ignition方法
                            //我是drive方法


 







