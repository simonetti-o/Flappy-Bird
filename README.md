# Flappy Bird 🐦

Jogo Flappy Bird com **ranking online** para competir com amigos!

## 🎮 Como jogar

- **Espaço / Clique / Toque** → o pássaro voa!
- Desvie dos canos verdes
- Quanto mais longe, maior a pontuação
- Salve seu nome no ranking e desafie seus amigos

---

## 🏆 Configurar o Ranking Online (Firebase)

O ranking online usa o **Firebase Realtime Database** (gratuito). Siga os passos abaixo:

### 1. Criar um projeto Firebase

1. Acesse [console.firebase.google.com](https://console.firebase.google.com) e faça login com sua conta Google
2. Clique em **"Adicionar projeto"**
3. Dê um nome (ex: `flappy-bird-ranking`) e finalize a criação

### 2. Ativar o Realtime Database

1. No menu lateral, clique em **Build → Realtime Database**
2. Clique em **"Create Database"**
3. Escolha a localização (pode deixar o padrão)
4. Selecione **"Start in test mode"** — isso permite leitura e escrita públicas (ideal para começar)
5. Clique em **Enable**

### 3. Obter as credenciais

1. No menu lateral, clique na engrenagem ⚙️ → **"Project settings"**
2. Role até **"Your apps"** e clique em **"</>"** (Web)
3. Dê um nome ao app (ex: `flappy-web`) e clique em **"Register app"**
4. Copie o objeto `firebaseConfig` exibido na tela

### 4. Colar as credenciais no jogo

Abra o arquivo `index.html` e localize o bloco `FIREBASE_CONFIG` (perto da linha 160):

```javascript
const FIREBASE_CONFIG = {
    apiKey:            "",   // <- cole aqui
    authDomain:        "",
    databaseURL:       "",   // <- obrigatorio para o ranking funcionar
    projectId:         "",
    storageBucket:     "",
    messagingSenderId: "",
    appId:             ""
};
```

Substitua os campos com os valores do seu projeto e salve o arquivo.

### 5. Publicar no GitHub Pages

1. Faça **commit e push** das alterações para o branch `main`
2. No GitHub, vá em **Settings → Pages**
3. Em **Source**, selecione o branch `main` e a pasta `/ (root)`
4. Clique em **Save** e aguarde alguns minutos
5. Acesse o link gerado (ex: `https://simonetti-o.github.io/Flappy-Bird/`) e compartilhe com seus amigos!

---

## 🔒 Regras de Segurança (Recomendado)

Para evitar que alguém insira pontuações absurdas, configure as regras no Firebase Console → Realtime Database → **Rules**:

```json
{
  "rules": {
    "scores": {
      ".read": true,
      ".write": true,
      "$score": {
        ".validate": "newData.hasChildren(['name', 'score', 'at']) &&
                      newData.child('name').isString() &&
                      newData.child('name').val().length >= 1 &&
                      newData.child('name').val().length <= 20 &&
                      newData.child('score').isNumber() &&
                      newData.child('score').val() >= 0 &&
                      newData.child('score').val() <= 9999"
      }
    }
  }
}
```

---

## 🛠️ Rodar localmente (Java)

```bash
cd src
javac App.java FlappyBird.java
java App
```

## Tecnologias

- Java Swing (versão desktop)
- HTML5 Canvas + JavaScript (versão web com ranking)
- Firebase Realtime Database (ranking online)
- GitHub Pages (hospedagem gratuita)
