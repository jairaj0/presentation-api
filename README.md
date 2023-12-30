**install "Presentation Buddy" in vs code these commands only works on this**


*** Commands ***
commands>>>
[
{ "file": ["open/create", "path"] },
{ "goto": ["line", "column"] },
{ "cmd": "save/wait manual time/number of delay time" },
{ "text": [code in text, "delay"] },
{ "linebyline": [code in text,[line , column] , "delay" , wait/1000 },
{ "css": [code in text,[line , column] , "delay" , wait/1000 },
{ "emmet": ["code in text" , "delay"] },
{ "line": [lineNo , no of lines] }
]

*** veriables for short-cut ***

commands>>>

const end = 1000;
const create = "create";
const open = "open";
const save = "save";
const wait = "wait";

*** example of commands send ***

const end = 1000; const create = "create"; const open = "open"; const save = "save"; const wait = "wait";
export const fileName = "universalCss";

export const commands = [
  your commands >>>

    { "file": ["open", "Styles/test.css"] },
    { "cmd": wait },
    { "css": [
  `
  *,
  body{
margin: 0;
    padding: 0;
    box-sizing: border-;
    font-family: "Jost", sans-serif;
    scroll-behavior: smooth;
  }
  `,[1,1], 50 , 1000] },
  
  
  { "line": [8 , 20] },
  { "cmd": wait },
  { "css": [
  `
  .text,
  .text * {
    font-family: "IBM Plex Mono", monospace;
  }
  `,[28,1], 50 , 100] },

  ]

*** how to start ***

// step 1 : run command

npm install axios fs

note :  add this to package.json
       "type": "module",

// step 2 : main.js

commands >>>

import axios from "axios";
import { commands, fileName } from "./index.js";
import fs from 'fs';

let data = JSON.stringify({"commands": commands }, null, 2);
const _path = `./Commands/${fileName}.json`;

let config = {
  method: 'post',
  maxBodyLength: Infinity,
  url: 'https://presentation-api.vercel.app/process-command',
  headers: { 
    'Content-Type': 'application/json'
  },
  data : data
};

axios.request(config)
.then((response) => {
  fs.writeFileSync(_path, JSON.stringify(response.data.commands, null, 2));

})
.catch((error) => {
  console.log(error);
});

// step 3 : create "Commands" folder

// step 4 : index.js

commands >>>
const end = 1000; const create = "create"; const open = "open"; const save = "save"; const wait = "wait";
// give any file name you want to store commands
export const fileName = "universalCss";

export const commands = [
    { "file": ["open", "Styles/test.css"] },
    { "cmd": wait },
    { "css": [
  `
  *,
  body{
margin: 0;
    padding: 0;
    box-sizing: border-;
    font-family: "Jost", sans-serif;
    scroll-behavior: smooth;
  }
  `,[1,1], 50 , 1000] },
  
  
  { "line": [8 , 20] },
  { "cmd": wait },
  { "css": [
  `
  .text,
  .text * {
    font-family: "IBM Plex Mono", monospace;
  }
  `,[28,1], 50 , 100] },
  ]

// step 5 : run command

    node main.js

check your Commands folder you will get your new json file
