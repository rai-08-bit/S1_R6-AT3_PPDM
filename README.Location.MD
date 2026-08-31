# S1_R6-AT3_PPDM
Objetivo da atividade
 - Esta é uma atividade que tem como objetivo, documentar a utilização e configuração do Expo Location.

## O Expo Location
### O que é?
 - É uma biblioteca da Expo que permite a leitura de informações de localização do dispositivo, ou seja, o usuário pode consultar a localização atual por meio desta biblioteca.

### Como instalar e implantar no aplicativo?
 - Antes da instalação da biblioteca é necessário verificar se o expo está instalado e pronto para uso, caso não esteja, no terminal, digite:
 - ```bash
    npm install -g expo-cli
    <!-- o '-g' significa que o expo será instalado globalmente -->
    ```

 - É possível instalar a biblioteca digitando o código abaixo no terminal
 - ```bash
    npx expo install expo-location
    <!-- instalando a biblioteca -->
    ```
 - Com a instalação concluída, para utilizar no desenvolvimento do aplicativo, é necessário que seja feita a importação da biblioteca.
 - Caso haja a necessidade de utilizar um emulador é preciso que antes seja certificado que a localização do mesmo esteja ativada e funcionando corretamente.
 - ```javascript
    import * as Location from 'expo-location'
    //importando a biblioteca do expo
    ```
 - Além da importação da biblioteca, é essencial a importação de outros componentes dos frameworks do Expo. Como:
 -  ```javascript
    import React, { useEffect, useState } from "react";
    import { StyleSheet, Text, View } from "react-native";
    import { SafeAreaView } from "react-native-safe-area-context";
    // importando componentes para a utilização
    ```
 - Após a instalação e importação dos componentes, bilbiotecas e frameworks, o exemplo abaixo é uma forma comum de utilização da biblioteca
 ```javascript
 export default function PosicaoGPSScreen() {
  const { location, setLocation } = useState(null);
  const { errorMsg, setErrorMsg } = useState(null);

  useEffect(() => {
    async function getCurrentLocation() {
      const { status } = await Location.requestForegroundPermissionsAsync();

      if (status !== 'granted') {
        setErrorMsg("Permissão negada")
        return;
      }
      const tempLocation = await Location.getCurrentPositionAsync();
      setLocation(tempLocation);
    }
    getCurrentLocation();

  }, []);

  let text = 'Aguardando...';
  if (errorMsg) {
    text = errorMsg;
  } else if (!errorMsg && location) {
    text = JSON.stringify(location);
  }
//retorna a função PosicaoGPSScreen
  return (
    <SafeAreaView style={styles.safeArea}>
      <View style={styles.container}>
        <View style={styles.header}>
          <Text style={styles.titleScreen}>Posição atual</Text>
          <Text style={styles.paragraph}>{text}</Text>
        </View>
      </View>
    </SafeAreaView>
  );
}
 ```

### Porquê utilizar o expo Location?
 - Ele é importante para a procura de localização em tempo real

<-- Eu tentei de verdade -->
