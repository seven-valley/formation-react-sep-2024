# Etape 1
## Personne.jsx
```jsx
export default function Personne() {
    return (
        <h1>Je suis le composant Personne</h1>
    )
}
```

## App.jsx
```jsx
import Personne from './components/Personne'
export default function App() {
  
  
  return (
    <>
    <Personne />
    <Personne />
    <Personne />
    </>
  );
}
```

# ETAPE 2 les props

## App.jsx
```jsx
import Personne from './components/Personne'
export default function App() {
  
  
  return (
    <>
    <Personne  prenom="Brad" nom="PITT"/>
    <Personne  prenom="Tom" nom="CRUISE"/>
    <Personne  prenom="Angelina" nom="Jolie"/>
    </>
  );
}
```


## Personne.jsx
```jsx
export default function Personne({prenom,nom}) {
    return (
        <h1>Je suis {prenom} {nom}</h1>
    )
}
```

# Etape 3 tableau d'objets

## App.jsx
```jsx
import Personne from './components/Personne'
export default function App() {
  const personnes =[
    {prenom:'Nicolas',nom:'CAGE'},
    {prenom:'Angelina',nom:'JOLIE'},
    {prenom:'Tom',nom:'Hanks'},
  ];
  // i c'est l indice : 0 , 1 ,2
  return (
    <>
        { personnes.map( (p,i) => <Personne key={i} nom={p.nom} prenom={p.prenom} />)}
    </>
  );
}
```
## Etape 4 props et fonctions

## App.jsx
```jsx
import Personne from './components/Personne'
export default function App() {
  const personnes =[
    {prenom:'Nicolas',nom:'CAGE'},
    {prenom:'Angelina',nom:'JOLIE'},
    {prenom:'Tom',nom:'Hanks'},
  ];
  const qui=(indice)=>{
    console.log(indice);
    console.log(personnes[indice]);
  }
  return (
    <>
     { personnes.map( (p,i) => <Personne 
     key={i} 
     nom={p.nom} prenom={p.prenom} 
     indice={i}
     qui={qui}
     />)}
    </>
  );
}
```

## Personne.jsx
```jsx
export default function Personne({prenom,nom,indice,qui}) {
    return (
        <p>{indice} Je suis {prenom} {nom}
        <button onClick={()=> qui(indice) }>Qui ?</button>
        </p>
        
    )
}
```

## Etape 5 props et fonctions

**App.jsx**
```jsx
import {useState} from 'react';
import Personne from './components/Personne'
export default function App() {
  const [personnes,setPersonnes] = useState([
    {nom:'PITT',prenom:'Brad'},
    {nom:'CRUISE',prenom:'Tom'},
    {nom:'JOLIE',prenom:'Angelina'},
  ]);
  const enlever=(indice)=>{
    personnes.splice(indice,1);
    setPersonnes([...personnes]);
  }
  return (
    <div className="container">
      <div className="col-4">
      <h2>Les personnes</h2>
				{personnes.map(
          (personne,indice)=><Personne 
          key={indice} 
          personne={personne} 
          indice={indice} 
          enlever={enlever}
          />)}
      </div>
    </div>

  );
}
```

**Personne.jsx**
```jsx
export default function Personne(props) {
    return (
       <p>
        {props.personne.prenom}
        {props.personne.nom}
        <button className="btn btn-danger" 
        onClick={()=>props.enlever(props.indice)}>OFF</button>
       </p>
        
    )
}
```

**Personne.jsx**
```jsx
export default function Personne({personne,indice,enlever}) {
    return (
       <p>
        {personne.prenom}
        {personne.nom}
        <button className="btn btn-danger" 
        onClick={()=>enlever(indice)}>OFF</button>
       </p>
        
    )
}
```