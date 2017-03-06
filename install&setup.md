
# Instalação e Setup {#install&setup}

Esta aplicação utiliza [NativeScript com TypeScript + Angular](http://docs.nativescript.org/angular/tutorial/ng-chapter-0).

## Pré-requisitos
Este guia pressupõe que o utilizar tenha algum conhecimento de JavaScript, CSS e o terminal de sua máquina de desenvolvimento. 
Recomenda-se a realização do seguinte tutorial [NativeScript: Get started with TypeScript and Angular 2](http://docs.nativescript.org/angular/tutorial/ng-chapter-0)

*Editor de texto recomendado* - Visual Studio Code, pois possui suporte de TypeScript incorporado

### terminal do MacOS 

####Step 1: Instalar Node.js
A CLI do NativeScript é baseada em Node.js e, como tal é necessário ter o Node.js instalado para usar o NativeScript.
Download dos ultimos updates do [Homebrew](https://brew.sh/)

```
brew update
``` 

```
brew install node@6
```


####Step 2: Instalar NativeScript CLI
```
npm install -g nativescript
```
Poderá verificar que a instalação foi concluida com sucesso ao correr o comando `tns`
```
$ tns
# NativeScript
┌─────────┬─────────────────────────────────────────────────────────────────────┐
│ Usage   │ Synopsis                                                            │
│ General │ $ tns <Command> [Command Parameters] [--command <Options>]          │
│ Alias   │ $ nativescript <Command> [Command Parameters] [--command <Options>] │
```

####Step 3: Clonar o repositório do VSTS
Depois de lhe serem garantidas as permissões necessarias para aceder ao repositório, deverá executar o seguinte comando:
```
git clone https://nma-spms.visualstudio.com/CeS/_git/CeS-App
```
Será solicitado que coloque o seu Username (xxx@spms.min-sade.pt) e respetiva palavra-passe.
####Step 4: Correr applicação

Este comando instala as dependencias listadas no npm caso ainda nao estejam instaladas
```
tns run android ou tns run ios

```