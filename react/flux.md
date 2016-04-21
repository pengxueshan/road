# 理解flux
1. flux的数据流向：动作（action） - 控制器（controller或者dispatcher） - 数据存储（store） - 视图（view，在react中为components） - 动作（action）

2. 一个动作比如点击按钮，将这个动作封装成一个对象（此对象包含动作类型和一些要改变的数据）传递给控制器，然后控制判断动作类型来选择要将动作传递给哪个store（Dispatcher 只用来派发 Action，不应该有其他逻辑，它的作用相当于一个路由，负责在action和store之间，建立action的正确传递路线，Dispatcher 只能有一个，而且是全局的），然后更新store的数据，触发相应的更新事件（一般store会继承EventEmitter，因此可以来监听和触发事件），在view层，我们事先定义好更新视图的逻辑，在components加载完成时（componentDidMount）注册，一旦store有变化，就会触发view的更新