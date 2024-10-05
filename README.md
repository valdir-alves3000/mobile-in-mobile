# Criando um App Expo com Termux

### Passo 1: Instalar o Termux

- Baixe o Termux pela Google Play Store ou do site [F-Droid](https://f-droid.org/en/packages/com.termux/).
- Abra o Termux.

### Passo 2: Atualizar Pacotes no Termux

Antes de instalar as ferramentas, atualize os pacotes:

```bash
pkg update && pkg upgrade
```

### Passo 3: Instalar Node.js e npm

O Expo precisa do Node.js para funcionar. Instale o Node.js e o npm com o seguinte comando:

```bash
pkg install nodejs
```

Verifique se a instalação foi bem-sucedida:

```bash
node -v
npm -v
```

### Passo 4: Instalar Expo CLI

Instale a Expo CLI globalmente com o npm:

```bash
npm install -g expo-cli
```

Verifique a versão:

```bash
expo --version
```

### Passo 5: Instalar Tmux

O `tmux` permite que você crie várias sessões de terminal em uma única janela e mantenha os processos ativos mesmo ao sair do Termux.

Instale o `tmux`:

```bash
pkg install tmux
```

Verifique a versão instalada:

```bash
tmux -V
```

### Passo 6: Criar um Projeto Expo

Agora podemos criar um projeto básico Expo. Navegue até o diretório desejado e crie um novo projeto:

```bash
expo init myApp
```

Escolha o template **blank** (vazio) e siga as instruções.

### Passo 7: Usar o Tmux para Sessões Persistentes e Navegação

#### 7.1. Criar uma Sessão Tmux:

Para iniciar o desenvolvimento em uma sessão `tmux`, execute:

```bash
tmux new -s expo-session
```

Dentro dessa sessão, você pode iniciar o servidor Expo:

```bash
cd myApp
expo start
```

#### 7.2. Criar e Navegar entre Telas no Tmux:

Com o `tmux`, você pode criar novas telas para facilitar o multitasking.

- **Criar uma Nova Tela**: 
  ```
  Ctrl + b, c
  ```

- **Alternar Entre Telas**: 
  - Para a próxima tela:
    ```
    Ctrl + b, n
    ```
  - Para a tela anterior:
    ```
    Ctrl + b, p
    ```

- **Listar Todas as Telas**:
  ```
  Ctrl + b, w
  ```

#### 7.3. Dividir a Tela em Painéis:

Para ver várias tarefas ao mesmo tempo, você pode dividir a tela.

- **Dividir Horizontalmente**:
  ```
  Ctrl + b, "
  ```

- **Dividir Verticalmente**:
  ```
  Ctrl + b, %
  ```

- **Navegar Entre Painéis**:
  ```
  Ctrl + b, seta
  ```

#### 7.4. Sair sem Fechar a Sessão:

Para sair da sessão `tmux` sem parar os processos:

```
Ctrl + b, d
```

Reentre a sessão a qualquer momento:

```bash
tmux attach -t expo-session
```

### Passo 8: Acessar Arquivos do Sistema Android no Termux

O Termux permite acessar e manipular arquivos no sistema Android. No entanto, por razões de segurança, você precisa conceder permissões para acessar os diretórios do Android, como **Downloads**, **Pictures**, etc.

#### 8.1. Conceder Permissão de Acesso ao Sistema de Arquivos:

Para permitir que o Termux acesse arquivos do sistema Android, execute:

```bash
termux-setup-storage
```

Isso criará uma pasta `storage` dentro do diretório home do Termux, com links simbólicos para vários diretórios do Android, como **Downloads**, **DCIM**, **Pictures**, etc.

#### 8.2. Acessar Diretórios do Android:

Depois de conceder as permissões, você poderá acessar os diretórios do Android a partir do Termux:

- **Acessar a pasta de downloads**:
  ```bash
  cd /storage/emulated/0/Download
  ```

- **Acessar imagens (pasta Pictures)**:
  ```bash
  cd /storage/emulated/0/Pictures
  ```

- **Acessar arquivos do cartão SD** (se houver):
  ```bash
  cd /storage/sdcard1
  ```

Agora, você pode copiar, mover e manipular arquivos nesses diretórios usando os comandos comuns do Linux como `cp`, `mv`, e `rm`.

#### 8.3. Exemplo de Cópia de Arquivo para a Pasta de Downloads:

Para copiar uma imagem para a pasta de **Downloads**, por exemplo, você pode usar o seguinte comando:

```bash
cp /path/to/image.png /storage/emulated/0/Download/
```

### Passo 9: Testar o App no Dispositivo

Depois de rodar o comando `expo start`, um QR code será gerado no terminal. Você pode escanear este QR code usando o aplicativo **Expo Go** em seu dispositivo Android ou iOS para visualizar o aplicativo.

Baixe o **Expo Go** na Play Store ou App Store.

### Conclusão

Agora você configurou um ambiente de desenvolvimento completo no Termux, com o `tmux` para gerenciar sessões e múltiplas telas, além de acesso aos arquivos do sistema Android. Isso permite que você trabalhe no desenvolvimento do seu aplicativo Expo enquanto gerencia arquivos diretamente no seu dispositivo.

### Comandos Resumidos:

1. **Atualizar pacotes**:
   ```bash
   pkg update && pkg upgrade
   ```

2. **Instalar Node.js e npm**:
   ```bash
   pkg install nodejs
   ```

3. **Instalar Expo CLI**:
   ```bash
   npm install -g expo-cli
   ```

4. **Instalar tmux**:
   ```bash
   pkg install tmux
   ```

5. **Criar projeto Expo**:
   ```bash
   expo init myApp
   ```

6. **Conceder permissão ao Termux para acessar arquivos**:
   ```bash
   termux-setup-storage
   ```

7. **Acessar diretórios do sistema Android**:
   - Downloads:
     ```bash
     cd /storage/emulated/0/Download
     ```
   - Pictures:
     ```bash
     cd /storage/emulated/0/Pictures
     ```

8. **Usar tmux**:
   - Criar nova sessão:
     ```bash
     tmux new -s expo-session
     ```
   - Criar nova tela: `Ctrl + b, c`
   - Alternar telas: `Ctrl + b, n` ou `Ctrl + b, p`
   - Dividir tela: `Ctrl + b, "` ou `Ctrl + b, %`
   - Sair sem encerrar a sessão: `Ctrl + b, d`
   - Reentrar na sessão:
     ```bash
     tmux attach -t expo-session
     ```


### Vamos criar um quadrado básico usando o `Animated.View` e o `StyleSheet`. 

```javascript
import React, {useRef} from "react";
import {StyleSheet, Text, View, PanResponder, Animated} from "react-native";

export default function App() {

  return (
    <View style={styles.container}>
      <Text style={styles.text}>Mobile in Mobile</Text>
      <Animated.View
        style={styles.square}
      />
    </View>
  );
};


const styles = StyleSheet.create({
  container: {
    flex: 1,
    alignItems: "center",
    justifyContent: "center",
    backgroundColor: "#41414d",
  },
  text: {
    fontSize: 32,
    marginBottom: 20,
    color: "#ccc"
  },
  square: {
    width: 150,
    height: 150,
    backgroundColor: "#ccc",
    borderRadius: "10%"
  },
});

```

### Agora vamos Adicionar a Animação de Arrastar

```javascript

  const pan = useRef(new Animated.ValueXY()).current;

  const panResponder = useRef(
    PanResponder.create({
      onStartShouldSetPanResponder: () => true,
      onPanResponderMove: Animated.event([null, {dx: pan.x, dy: pan.y}], {
        useNativeDriver: false,
      }),
      onPanResponderRelease: () => {
        Animated.spring(pan, {
          toValue: {x: 0, y: 0},
          useNativeDriver: false,
        }).start();
      },
    }),
  ).current;

  ```

  ```javascript
<Animated.View
    style={[
      styles.square,
      {transform: [{translateX: pan.x}, {translateY: pan.y}]},
    ]}
    {...panResponder.panHandlers}
  />

```



