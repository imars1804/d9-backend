use ecommerce

db.createCollection("mensajes");
db.createCollection("productos");

//1
db.mensajes.insertMany([
  { email: "lalilupinacci@gmail.com", date: new Date(), text: "Hola, todo bien?" },
  { email: "random@gmail.com", date: new Date(), text: "Hola Lali! Todo bien y vos?" },
  { email: "random@gmail.com", date: new Date(), text: "Como la pasaste este fin de semana?" },
  { email: "lalilupinacci@gmail.com", date: new Date(), text: "La verdad que muy bien!" },
  { email: "lalilupinacci@gmail.com", date: new Date(), text: "Y vos?" },
  { email: "random@gmail.com", date: new Date(), text: "Muy bien tambien!" },
  { email: "random@gmail.com", date: new Date(), text: "Me fui a la costa con amigos, asi que estuvo a full" },
  { email: "random@gmail.com", date: new Date(), text: "Che estoy muuy cansado!" },
  { email: "random@gmail.com", date: new Date(), text: "Me voy a ir a dormir, nos vemos mañana!" },
  { email: "lalilupinacci@gmail.com", date: new Date(), text: "Dale, nos vemos!" },
]);

//2
db.productos.insertMany([
    { title: "Avatar: The Way of Water", price: 999, url: "https://pbs.twimg.com/media/FiHA41XVsAQYjS4?format=jpg&name=900x900" },
    { title: "Avengers 1", price: 900, url: "https://i0.wp.com/noescinetodoloquereluce.com/wp-content/uploads/2015/02/avengers-1.jpg?ssl=1" },
    { title: "Avatar", price: 1550, url: "https://i.pinimg.com/originals/6d/aa/c2/6daac2a42ad7d987c6c102eb88fd94eb.jpg" },
    { title: "Yo antes de ti", price: 670, url: "https://pbs.twimg.com/media/CaOKqerXEAACYWN.jpg" },
    { title: "Rápidos y Furiosos 7", price: 4578, url: "https://www.themoviedb.org/t/p/original/wnfQmn1f1v0P8I27F2qsqOM462Q.jpg" },
    { title: "Spiderman: No Way Home", price: 5000, url: "https://img.ecartelera.com/noticias/fotos/70100/70190/1.jpg" },
    { title: "Iron Man 1", price: 158, url: "https://i.pinimg.com/originals/10/f9/cc/10f9cc09b38a919f656a0912c0d5612c.jpg" },
    { title: "Avengers: End Game", price: 4999, url: "https://quenoticias.com/wp-content/uploads/2019/03/AvengersEndgame.jpg" },
    { title: "Avengers: Infinity War", price: 2854, url: "https://pbs.twimg.com/media/DamPnPIV4AAzaWn.jpg:large" },
    { title: "Guardians of the Galaxy: Vol. 1", price: 1653, url: "https://m.media-amazon.com/images/I/71lbFfxfMtL._AC_UF894,1000_QL80_.jpg" },
]);

//3
db.mensajes.find().pretty();
db.productos.find().pretty();

//4
db.mensajes.estimatedDocumentCount();
db.productos.estimatedDocumentCount();

//5
//A)
db.productos.insertOne({ title: "Spiderman: Homecoming", price: 4999, url: "https://static.wikia.nocookie.net/marvelcinematicuniverse/images/4/43/Spider-Man_Homecoming_-_Poster_INT_2.png/revision/latest?cb=20191029195957&path-prefix=es" });

//B)
//i)
db.productos.find({"price": {$lt: 1000}}).pretty()
//ii)
db.productos.find({ $and: [{"price": {$gte: 1000}}, {"price": {$lte: 3000}}]}).pretty()
//iii)
db.productos.find({"price": {$gt: 3000}}).pretty()
//iv)
db.productos.find({},{"title": 1, "_id": 0}).sort({"price": 1}).skip(2).limit(1).pretty()

//C)
db.productos.updateMany({}, {$set: {"stock": 100}})

//D)
db.productos.updateMany({"price": {$gt: 4000}}, {$set: {"stock": 0}})

//E)
db.productos.deleteMany({"price": {$lt: 1000}})

//6)
use admin;
db.createUser({ user : "pepe", pwd : "asd456", roles : [{ role : "read", db : "ecommerce" }] });