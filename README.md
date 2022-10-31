# Writing Test Week 1 Front-End Bootcamp
## React.js
- React : sebuah library untuk membuat tampilan website
- React JS dibuat oleh Tim Engineer Facebook
- keuntungan/kelebihan dari react : Lebih proses cepetnya, misalkan : bikin navbar cukup sekali aja, tidak perlu meng-copas pada codingan tampilan yang lain hanya cukup dipanggil saja navbarnya
- Banyak aplikasi yang dibuat dengan menggunakan react, contohnya fb, ig, uber, twitter
- Java Script hanya bisa berjalan di web browser
- Jadi di dalam browser ada mesin JS yang berjalan didalam web browser, dan NodeJS dapat berjalan diluar browser
- NodeJS adalah aplikasi untuk menajalankan react.js
- Framework java script selain react JS, ada : vue, angular, svelte
### cara mendownload reactJS
1. download NodeJS
2. install nodeJS
3. jika NodeJS sudah terinstall, selanjutnya buat folder baru, beri nama folder
4. klik kanan, pilih git bash
5. ketik "npx create-react-app (nama folder)"
6. maka selanjutnya akan ada proses download
7. tunggu sampai proses download selesai
8. proses download selesai, ditandai dengan tulisan "Happy Hacking!"
### cara menggunakan ReactJS
- buka vs code
- lalu buka terminal, ketik npm start
- buka yang file src
- lalu buka App.js
- kita ngoding di dalam App.js, di dalam function App
- function App () hanya bisa menampung satu element
 ```js
 //index.js
import React from 'react';
import ReactDOM from 'react-dom/client';
import './index.css';
import App from './App';
import reportWebVitals from './reportWebVitals';

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);

// If you want to start measuring performance in your app, pass a function
// to log results (for example: reportWebVitals(console.log))
// or send to an analytics endpoint. Learn more: https://bit.ly/CRA-vitals
reportWebVitals();


 //App.js
 import './App.css';
 
 function App(){
  return(
    <h1>Syifa</h1>   //output : Syifa
  )
}

export default App;
 ```

- penulisan function di react harus pakai huruf besar diawal. 
```js
function App()
```
- harus ada return
```js
function App(){
  return()
}
```
- hanya boleh ada 1 parent utama <div></div> atau pake tag kosong
```js
//App.js
function App(){
  return(
  <>
    <h1>Syifa</h1>
  </>
  )
}
```
- Jika ingin pakai pake boostrap, bisa download cdn atau download di npm, lalu pasang di html
- di react 'class' tidak ada, adanya className
```js
//App.jsx
import "./App.css";
function App(){
  return(
  <>
    <div>img src="" alt="" className="profile-img"/>
    </div>
  </>
  );
}
```
```css
//App.css
.profile-img{
 width: 150px;
 height: 150px;
 overflow: hidden;
 border-radius: 100%
 object-fit: cover;
}
```
## State dan Props
- component adalah bagian2 dari sebuah website
- state : data yg tinggal di dalam komponen tersebut
- props data yang dikasih/pemberian dat. Digunakan untuk komunikasi dari components parent dan child ngirim sebuah parameter di function
- state adalah sebuah object untuk menyimpan data di react
- prosesnya : data ditampung di state, kemudian dikirim melalu props
- props dipasang di function
```js
//buat file baru didalam components, dengan nama MemberInfo.jsx
//MemberInfo.jsx
const MemberInfo = (props) => {
 return (
  <div className="profile-container">
   <img src="" alt="" className=""/>
   <div className="profile-info">
    <h2>{}/h2>
    <h3>22 tahun</h3>
    <p>peserta bootcamp frontend</p>
   </div>
  </div>
 )
}
```
```js
//App.jsx
import"./App.css";
import Memberinfo from "./components/MemberInfo";

function App(){
 return(
  <>
   <MemberInfo/>    //output : memangggil data dari MemberInfo
  </>
 );
}
```
#### Event-handler
- useState untuk menyimpan data yg sifatnya berubah2
```main.jsx
//main.jsx
import React from 'react'
import ReactDOM from 'react-dom/client'
import App from './App'
// import style
import 'bootstrap/dist/css/bootstrap.min.css';

ReactDOM.createRoot(document.getElementById('root')).render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
)
```
```js
//App.jsx
import { useState } from "react";
import Card from "./components/Card";
import Counter from "./components/Counter";
import ListUser from "./components/ListUser";

function App() {
  // utk conditional rendering
  const [isLogin, setIsLogin] = useState(false);

  return (
    <div>
      {/* munculin button klo belum login */}
      {!isLogin && <button onClick={() => setIsLogin(true)}>Login</button>}

      <br />

      {/* jika sudah login, munculkan counter  */}
      {isLogin ? <Counter /> : <span>login dulu cuuuy...</span>}

      {/* jika sudah login, munculkan ListUser  */}
      {isLogin && <ListUser />}

    </div>
  );
}

export default App;
```
### Life Cycle
- ada 3 Siklus : Mount, update, unmount
- Membuat component ada 2 cara :
 1. Function component
 2. class component
  - yang ada pada class component
   1. componentDidMount
   2. componentDidUpdate
   3. componentWillUnmount 
- use effect : memberikan efek samping/untuk memperlihatkan apa yang terjadi ketika datanya berubah
```js
//main.jsx
import React from 'react'
import ReactDOM from 'react-dom/client'
import App from './App'

ReactDOM.createRoot(document.getElementById('root')).render(
  // <React.StrictMode>
    <App />
  // </React.StrictMode>
)
```
```jsx
//ListDigimon.jsx
import{useEffect} from "react";
function ListDigimon(){
 console.log("List Digimon dipanggil");  //output pada console : List Digimon dipanggil
 useEffect(() => {
  console.log("ListDigimon mount")  //output pada console : ListDigimon mount
 })

 return(
  <>
   <h1>Hallo</h1>  //output : Hallo
  </>
 )
}

export default ListDigimon
```
- pada kodingan diatas, proses pertama yang ditampilkan adalah List Digimon dipanggil, kemudian Hallo, dan yang terakhir ListDigimon mount
- pada tiap life cycle, kita dapat menambahkan efek yang diperlukan, contohnya :
  - ketika komponen mucul, ambil data pakai fetch
  - ketika data state berubah, lakukan filter
  - ketika komponen hilang, data state jangan diupdate
```jsx
//ListDigimon.jsx
import{useEffect, useState} from "react";
function ListDigimon(){
 const [isLoading, setIsLoading] = useState(false)
 console.log("List Digimon dipanggil");  //output pada console : List Digimon dipanggil
 useEffect(() => {
  console.log("ListDigimon mount")  //output pada console : ListDigimon mount
 })

 return(
  <>
   <h1>Hallo</h1>
   <button onClick={() => setIsLoading(!isLoading)} ubah loading</>
   <span>{isLoading + ""}</span>
  </>
 )
}

export default ListDigimon
```
- output 
 ![Screenshot (3324)](https://user-images.githubusercontent.com/114098894/198884859-ce4c3d13-50c3-4e5a-b5f2-7e1c15dd3815.png)
- ketika button ubah loading di klik, maka tulisan false akan berubah menjadi true dan seterusnya
```jsx
//ListDigimon.jsx
import axios from "axios";  
import{useEffect, useState} from "react";
function ListDigimon(){
 const [isLoading, setIsLoading] = useState(false)
 const [digimons, setdigimons] = useState([])
 console.log("List Digimon dipanggil");  //output pada console : List Digimon dipanggil
 useEffect(() => {
  console.log("ListDigimon mount")  //output pada console : ListDigimon mount
  axios("https://digimon-api.vercel.app/api/digimon") //axios digunakan sebagai pengganti fetch
  .then(res=> {
  setDigimosn(res.data))
}, []); //tanpa [] dijalankan berkali2 (mount dan update), pakai [] dijalankan 1x aja (mount)

console.log(digimons);
 return(
  <>
   <h1>Hallo</h1>
   <button onClick={() => setIsLoading(!isLoading)} ubah loading</>
   <span>{isLoading + ""}</span>
   {digimons.map()}  //output pada console : menampilkan secara rinci data2 pada digimons
  </>
 )
}

export default ListDigimon
```

```jsx
import React from "react";
import Form from "./components/Form";

const App = () => {
  return (
    <>
      <h1>Halo pagiii</h1> 
      <Form />
    </>
  );
};

export default App;
```
```jsx
//Form.jsx
import { useState } from "react";
import axios from "axios";

const Form = () => {
  const [name, setName] = useState(""); //kalo mau nampilin gapake set, pakenya yang kiri. buat ngeganti data, pake setData
  const [address, setAddress] = useState("");
  const [program, setProgram] = useState("");
  const [data, setData] = useState({});

  //   console.log(name, address);

  const handleSubmit = (e) => {
    e.preventDefault(); //fungsinya biar halaman ga ngerefresh pas input submit
    // setData({ name, address, program });
    // setName("");
    // setAddress("");
    // setProgram("");

    // proses post data menggunakan axios
    axios
      .post("http://localhost:3000/student", {
        name,
        address,
        program,
      })
      .then(() => {
        setData({ name, address, program });
        setName("");
        setAddress("");
        setProgram("");
      })
      .catch((err) => {
        console.log(err);
      });
  };

  return (
    <>
      <form action="" onSubmit={handleSubmit}> //ketika submit biar datanya keambil pake onSubmit
        <label htmlFor="name">Name</label>
        <input type="text" value={name} onChange={(e) => setName(e.target.value)} /> //onChange fungsinya untuk nangkap semua data yang ada didalam submit
        <label htmlFor="address">Address</label>
        <input type="text" value={address} onChange={(e) => setAddress(e.target.value)} /> //e.target.value fungsinya untuk nangkap semua data yang ada didalam submit
        <label htmlFor="option">Program</label>
        <select value={program} onChange={(e) => setProgram(e.target.value)}> 
          <option value="">select program</option>
          <option value="KM">KM</option>
          <option value="SIC">SIC</option>
          <option value="Amman">Amman</option>
        </select>
        <button type="submit">Submit</button>
      </form>

      <br />
      <h2>Name: {data.name}</h2>
      <h2>Address: {data.address}</h2>
      <h2>Program: {data.program}</h2>
    </>
  );
};

export default Form;
```
- output
- ![Screenshot (3364)](https://user-images.githubusercontent.com/114098894/198935242-bb41b91a-7617-4108-b8b8-094952ee4486.png)




