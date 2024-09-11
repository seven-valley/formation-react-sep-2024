# Module 5 le two ways binding - liaison bidirectionel
![module-5](../img/05/module-5.png)

# Exemple 1 : 2 ways binding
```jsx
export default function App() {
  const affiche =(event)=>{
    console.log(event.target.value);
  }
  
  return (
   
     <input onChange={affiche} />

  )
}

```
# Exemple 2 : useRef Versus useState
```jsx
import { useRef,useState } from "react";
export default function App() {
  const valeur = useRef(0); // valeur.curent =0
  const [nombre,setNombre] = useState(0);
  const ajouter = () => {
    valeur.current = valeur.current + 1;
    console.log(valeur.current);
  };
  const ajouter2 = () => {
  
  
   setNombre(nombre+1)
  };


  return (
    <>
      <button onClick={ajouter}>go</button>
      <button onClick={ajouter2}>go2</button>
      <br />

      <h1>useRef : {valeur.current}</h1>
      
      <h1>useState : {nombre}</h1>
    </>
  );
}

```

## ETAPE 1
Modifier le code ci dessus  
enlever le champ info  
ajouter un champ input prenom  
ajouter un champ input nom  
Afficher en temps réels le nom et le prénom  
```jsx
import "./App.css";
import { useRef, useState } from "react";
export default function App() {
  const prenom = useRef("");
  const nom = useRef("");
  const [info, setInfo] = useState("");
  const affiche = (e) => {
    if (e.target.name == 'nom'){
      //obj[e.target.name]= e.target.value;
      nom.current = e.target.value;
    }else{
      prenom.current = e.target.value;
    }
   // setInfo(prenom.current + ' '+nom.current);
    setInfo(`${prenom.current} ${nom.current}`);
  };
  return (
    <>
      <div className="container">
        <div className="col-4">
          <h1>Saisir votre nom</h1>
          <input
            className="my-3 form-control"
            name="prenom"
            onChange={affiche}
            placeholder="Prénom"
          />
          <input
            className="form-control"
            name="nom"
            onChange={affiche}
            placeholder="Nom"
          />
          <h1>{info}</h1>
        </div>
      </div>
    </>
  );
}
```
