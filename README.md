<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Interactive BOM for KiCAD</title>
  <style type="text/css">
:root {
  --pcb-edge-color: black;
  --pad-color: #878787;
  --pad-hole-color: #CCCCCC;
  --pad-color-highlight: #D04040;
  --pad-color-highlight-both: #D0D040;
  --pad-color-highlight-marked: #44a344;
  --pin1-outline-color: #ffb629;
  --pin1-outline-color-highlight: #ffb629;
  --pin1-outline-color-highlight-both: #fcbb39;
  --pin1-outline-color-highlight-marked: #fdbe41;
  --silkscreen-edge-color: #aa4;
  --silkscreen-polygon-color: #4aa;
  --silkscreen-text-color: #4aa;
  --fabrication-edge-color: #907651;
  --fabrication-polygon-color: #907651;
  --fabrication-text-color: #a27c24;
  --track-color: #def5f1;
  --track-color-highlight: #D04040;
  --zone-color: #def5f1;
  --zone-color-highlight: #d0404080;
}

html,
body {
  margin: 0px;
  height: 100%;
  font-family: Verdana, sans-serif;
}

.dark.topmostdiv {
  --pcb-edge-color: #eee;
  --pad-color: #808080;
  --pin1-outline-color: #ffa800;
  --pin1-outline-color-highlight: #ccff00;
  --track-color: #42524f;
  --zone-color: #42524f;
  background-color: #252c30;
  color: #eee;
}

button {
  background-color: #eee;
  border: 1px solid #888;
  color: black;
  height: 44px;
  width: 44px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 14px;
  font-weight: bolder;
}

.dark button {
  /* This will be inverted */
  background-color: #c3b7b5;
}

button.depressed {
  background-color: #0a0;
  color: white;
}

.dark button.depressed {
  /* This will be inverted */
  background-color: #b3b;
}

button:focus {
  outline: 0;
}

button#tb-btn {
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 8.47 8.47'%3E%3Crect transform='translate(0 -288.53)' ry='1.17' y='288.8' x='.27' height='7.94' width='7.94' fill='%23f9f9f9'/%3E%3Cg transform='translate(0 -288.53)'%3E%3Crect width='7.94' height='7.94' x='.27' y='288.8' ry='1.17' fill='none' stroke='%23000' stroke-width='.4' stroke-linejoin='round'/%3E%3Cpath d='M1.32 290.12h5.82M1.32 291.45h5.82' fill='none' stroke='%23000' stroke-width='.4'/%3E%3Cpath d='M4.37 292.5v4.23M.26 292.63H8.2' fill='none' stroke='%23000' stroke-width='.3'/%3E%3Ctext font-weight='700' font-size='3.17' font-family='sans-serif'%3E%3Ctspan x='1.35' y='295.73'%3EF%3C/tspan%3E%3Ctspan x='5.03' y='295.68'%3EB%3C/tspan%3E%3C/text%3E%3C/g%3E%3C/svg%3E%0A");
}

button#lr-btn {
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 8.47 8.47'%3E%3Crect transform='translate(0 -288.53)' ry='1.17' y='288.8' x='.27' height='7.94' width='7.94' fill='%23f9f9f9'/%3E%3Cg transform='translate(0 -288.53)'%3E%3Crect width='7.94' height='7.94' x='.27' y='288.8' ry='1.17' fill='none' stroke='%23000' stroke-width='.4' stroke-linejoin='round'/%3E%3Cpath d='M1.06 290.12H3.7m-2.64 1.33H3.7m-2.64 1.32H3.7m-2.64 1.3H3.7m-2.64 1.33H3.7' fill='none' stroke='%23000' stroke-width='.4'/%3E%3Cpath d='M4.37 288.8v7.94m0-4.11h3.96' fill='none' stroke='%23000' stroke-width='.3'/%3E%3Ctext font-weight='700' font-size='3.17' font-family='sans-serif'%3E%3Ctspan x='5.11' y='291.96'%3EF%3C/tspan%3E%3Ctspan x='5.03' y='295.68'%3EB%3C/tspan%3E%3C/text%3E%3C/g%3E%3C/svg%3E%0A");
}

button#bom-btn {
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 8.47 8.47'%3E%3Crect transform='translate(0 -288.53)' ry='1.17' y='288.8' x='.27' height='7.94' width='7.94' fill='%23f9f9f9'/%3E%3Cg transform='translate(0 -288.53)' fill='none' stroke='%23000' stroke-width='.4'%3E%3Crect width='7.94' height='7.94' x='.27' y='288.8' ry='1.17' stroke-linejoin='round'/%3E%3Cpath d='M1.59 290.12h5.29M1.59 291.45h5.33M1.59 292.75h5.33M1.59 294.09h5.33M1.59 295.41h5.33'/%3E%3C/g%3E%3C/svg%3E");
}

button#bom-grouped-btn {
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='32' height='32'%3E%3Cg stroke='%23000' stroke-linejoin='round' class='layer'%3E%3Crect width='29' height='29' x='1.5' y='1.5' stroke-width='2' fill='%23fff' rx='5' ry='5'/%3E%3Cpath stroke-linecap='square' stroke-width='2' d='M6 10h4m4 0h5m4 0h3M6.1 22h3m3.9 0h5m4 0h4m-16-8h4m4 0h4'/%3E%3Cpath stroke-linecap='null' d='M5 17.5h22M5 26.6h22M5 5.5h22'/%3E%3C/g%3E%3C/svg%3E");
}

button#bom-ungrouped-btn {
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='32' height='32'%3E%3Cg stroke='%23000' stroke-linejoin='round' class='layer'%3E%3Crect width='29' height='29' x='1.5' y='1.5' stroke-width='2' fill='%23fff' rx='5' ry='5'/%3E%3Cpath stroke-linecap='square' stroke-width='2' d='M6 10h4m-4 8h3m-3 8h4'/%3E%3Cpath stroke-linecap='null' d='M5 13.5h22m-22 8h22M5 5.5h22'/%3E%3C/g%3E%3C/svg%3E");
}

button#bom-netlist-btn {
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='32' height='32'%3E%3Cg fill='none' stroke='%23000' class='layer'%3E%3Crect width='29' height='29' x='1.5' y='1.5' stroke-width='2' fill='%23fff' rx='5' ry='5'/%3E%3Cpath stroke-width='2' d='M6 26l6-6v-8m13.8-6.3l-6 6v8'/%3E%3Ccircle cx='11.8' cy='9.5' r='2.8' stroke-width='2'/%3E%3Ccircle cx='19.8' cy='22.8' r='2.8' stroke-width='2'/%3E%3C/g%3E%3C/svg%3E");
}

button#copy {
  background-image: url("data:image/svg+xml,%3Csvg height='48' viewBox='0 0 48 48' width='48' xmlns='http://www.w3.org/2000/svg'%3E%3Cpath d='M0 0h48v48h-48z' fill='none'/%3E%3Cpath d='M32 2h-24c-2.21 0-4 1.79-4 4v28h4v-28h24v-4zm6 8h-22c-2.21 0-4 1.79-4 4v28c0 2.21 1.79 4 4 4h22c2.21 0 4-1.79 4-4v-28c0-2.21-1.79-4-4-4zm0 32h-22v-28h22v28z'/%3E%3C/svg%3E");
  background-position: 6px 6px;
  background-repeat: no-repeat;
  background-size: 26px 26px;
  border-radius: 6px;
  height: 40px;
  width: 40px;
  margin: 10px 5px;
}

button#copy:active {
  box-shadow: inset 0px 0px 5px #6c6c6c;
}

textarea.clipboard-temp {
  position: fixed;
  top: 0;
  left: 0;
  width: 2em;
  height: 2em;
  padding: 0;
  border: None;
  outline: None;
  box-shadow: None;
  background: transparent;
}

.left-most-button {
  border-right: 0;
  border-top-left-radius: 6px;
  border-bottom-left-radius: 6px;
}

.middle-button {
  border-right: 0;
}

.right-most-button {
  border-top-right-radius: 6px;
  border-bottom-right-radius: 6px;
}

.button-container {
  font-size: 0;
  margin: 10px 10px 10px 0px;
}

.dark .button-container {
  filter: invert(1);
}

.button-container button {
  background-size: 32px 32px;
  background-position: 5px 5px;
  background-repeat: no-repeat;
}

@media print {
  .hideonprint {
    display: none;
  }
}

canvas {
  cursor: crosshair;
}

canvas:active {
  cursor: grabbing;
}

.fileinfo {
  width: 100%;
  max-width: 1000px;
  border: none;
  padding: 5px;
}

.fileinfo .title {
  font-size: 20pt;
  font-weight: bold;
}

.fileinfo td {
  overflow: hidden;
  white-space: nowrap;
  max-width: 1px;
  width: 50%;
  text-overflow: ellipsis;
}

.bom {
  border-collapse: collapse;
  font-family: Consolas, "DejaVu Sans Mono", Monaco, monospace;
  font-size: 10pt;
  table-layout: fixed;
  width: 100%;
  margin-top: 1px;
  position: relative;
}

.bom th,
.bom td {
  border: 1px solid black;
  padding: 5px;
  word-wrap: break-word;
  text-align: center;
  position: relative;
}

.dark .bom th,
.dark .bom td {
  border: 1px solid #777;
}

.bom th {
  background-color: #CCCCCC;
  background-clip: padding-box;
}

.dark .bom th {
  background-color: #3b4749;
}

.bom tr.highlighted:nth-child(n) {
  background-color: #cfc;
}

.dark .bom tr.highlighted:nth-child(n) {
  background-color: #226022;
}

.bom tr:nth-child(even) {
  background-color: #f2f2f2;
}

.dark .bom tr:nth-child(even) {
  background-color: #313b40;
}

.bom tr.checked {
  color: #1cb53d;
}

.dark .bom tr.checked {
  color: #2cce54;
}

.bom tr {
  transition: background-color 0.2s;
}

.bom .numCol {
  width: 30px;
}

.bom .value {
  width: 15%;
}

.bom .quantity {
  width: 65px;
}

.bom th .sortmark {
  position: absolute;
  right: 1px;
  top: 1px;
  margin-top: -5px;
  border-width: 5px;
  border-style: solid;
  border-color: transparent transparent #221 transparent;
  transform-origin: 50% 85%;
  transition: opacity 0.2s, transform 0.4s;
}

.dark .bom th .sortmark {
  filter: invert(1);
}

.bom th .sortmark.none {
  opacity: 0;
}

.bom th .sortmark.desc {
  transform: rotate(180deg);
}

.bom th:hover .sortmark.none {
  opacity: 0.5;
}

.bom .bom-checkbox {
  width: 30px;
  position: relative;
  user-select: none;
  -moz-user-select: none;
}

.bom .bom-checkbox:before {
  content: "";
  position: absolute;
  border-width: 15px;
  border-style: solid;
  border-color: #51829f transparent transparent transparent;
  visibility: hidden;
  top: -15px;
}

.bom .bom-checkbox:after {
  content: "Double click to set/unset all";
  position: absolute;
  color: white;
  top: -35px;
  left: -26px;
  background: #51829f;
  padding: 5px 15px;
  border-radius: 8px;
  white-space: nowrap;
  visibility: hidden;
}

.bom .bom-checkbox:hover:before,
.bom .bom-checkbox:hover:after {
  visibility: visible;
  transition: visibility 0.2s linear 1s;
}

.split {
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
  overflow-y: auto;
  overflow-x: hidden;
  background-color: inherit;
}

.split.split-horizontal,
.gutter.gutter-horizontal {
  height: 100%;
  float: left;
}

.gutter {
  background-color: #ddd;
  background-repeat: no-repeat;
  background-position: 50%;
  transition: background-color 0.3s;
}

.dark .gutter {
  background-color: #777;
}

.gutter.gutter-horizontal {
  background-image: url('data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAUAAAAeCAYAAADkftS9AAAAIklEQVQoU2M4c+bMfxAGAgYYmwGrIIiDjrELjpo5aiZeMwF+yNnOs5KSvgAAAABJRU5ErkJggg==');
  cursor: ew-resize;
  width: 5px;
}

.gutter.gutter-vertical {
  background-image: url('data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAB4AAAAFAQMAAABo7865AAAABlBMVEVHcEzMzMzyAv2sAAAAAXRSTlMAQObYZgAAABBJREFUeF5jOAMEEAIEEFwAn3kMwcB6I2AAAAAASUVORK5CYII=');
  cursor: ns-resize;
  height: 5px;
}

.searchbox {
  float: left;
  height: 40px;
  margin: 10px 5px;
  padding: 12px 32px;
  font-family: Consolas, "DejaVu Sans Mono", Monaco, monospace;
  font-size: 18px;
  box-sizing: border-box;
  border: 1px solid #888;
  border-radius: 6px;
  outline: none;
  background-color: #eee;
  transition: background-color 0.2s, border 0.2s;
  background-image: url('data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABAAAAAQCAYAAAAf8/9hAAABNklEQVQ4T8XSMUvDQBQH8P/LElFa/AIZHcTBQSz0I/gFstTBRR2KUC4ldDxw7h0Bl3RRUATxi4iiODgoiLNrbQYp5J6cpJJqomkX33Z37/14d/dIa33MzDuYI4johOI4XhyNRteO46zNYjDzAxE1yBZprVeZ+QbAUhXEGJMA2Ox2u4+fQIa0mPmsCgCgJYQ4t7lfgF0opQYAdv9ABkKI/UnOFCClXKjX61cA1osQY8x9kiRNKeV7IWA3oyhaSdP0FkAtjxhj3hzH2RBCPOf3pzqYHCilfAAX+URm9oMguPzeWSGQvUcMYC8rOBJCHBRdqxTo9/vbRHRqi8bj8XKv1xvODbiuW2u32/bvf0SlDv4XYOY7z/Mavu+nM1+BmQ+NMc0wDF/LprP0DbTWW0T00ul0nn4b7Q87+X4Qmfiq2wAAAABJRU5ErkJggg==');
  background-position: 10px 10px;
  background-repeat: no-repeat;
}

.dark .searchbox {
  background-color: #111;
  color: #eee;
}

.searchbox::placeholder {
  color: #ccc;
}

.dark .searchbox::placeholder {
  color: #666;
}

.filter {
  width: calc(60% - 64px);
}

.reflookup {
  width: calc(40% - 10px);
}

input[type=text]:focus {
  background-color: white;
  border: 1px solid #333;
}

.dark input[type=text]:focus {
  background-color: #333;
  border: 1px solid #ccc;
}

mark.highlight {
  background-color: #5050ff;
  color: #fff;
  padding: 2px;
  border-radius: 6px;
}

.dark mark.highlight {
  background-color: #76a6da;
  color: #111;
}

.menubtn {
  background-color: white;
  border: none;
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='36' height='36' viewBox='0 0 20 20'%3E%3Cpath fill='none' d='M0 0h20v20H0V0z'/%3E%3Cpath d='M15.95 10.78c.03-.25.05-.51.05-.78s-.02-.53-.06-.78l1.69-1.32c.15-.12.19-.34.1-.51l-1.6-2.77c-.1-.18-.31-.24-.49-.18l-1.99.8c-.42-.32-.86-.58-1.35-.78L12 2.34c-.03-.2-.2-.34-.4-.34H8.4c-.2 0-.36.14-.39.34l-.3 2.12c-.49.2-.94.47-1.35.78l-1.99-.8c-.18-.07-.39 0-.49.18l-1.6 2.77c-.1.18-.06.39.1.51l1.69 1.32c-.04.25-.07.52-.07.78s.02.53.06.78L2.37 12.1c-.15.12-.19.34-.1.51l1.6 2.77c.1.18.31.24.49.18l1.99-.8c.42.32.86.58 1.35.78l.3 2.12c.04.2.2.34.4.34h3.2c.2 0 .37-.14.39-.34l.3-2.12c.49-.2.94-.47 1.35-.78l1.99.8c.18.07.39 0 .49-.18l1.6-2.77c.1-.18.06-.39-.1-.51l-1.67-1.32zM10 13c-1.65 0-3-1.35-3-3s1.35-3 3-3 3 1.35 3 3-1.35 3-3 3z'/%3E%3C/svg%3E%0A");
  background-position: center;
  background-repeat: no-repeat;
}

.statsbtn {
  background-color: white;
  border: none;
  background-image: url("data:image/svg+xml,%3Csvg width='36' height='36' xmlns='http://www.w3.org/2000/svg'%3E%3Cpath d='M4 6h28v24H4V6zm0 8h28v8H4m9-16v24h10V5.8' fill='none' stroke='%23000' stroke-width='2'/%3E%3C/svg%3E");
  background-position: center;
  background-repeat: no-repeat;
}

.iobtn {
  background-color: white;
  border: none;
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='36' height='36'%3E%3Cpath fill='none' stroke='%23000' stroke-width='2' d='M3 33v-7l6.8-7h16.5l6.7 7v7H3zM3.2 26H33M21 9l5-5.9 5 6h-2.5V15h-5V9H21zm-4.9 0l-5 6-5-6h2.5V3h5v6h2.5z'/%3E%3Cpath fill='none' stroke='%23000' d='M6.1 29.5H10'/%3E%3C/svg%3E");
  background-position: center;
  background-repeat: no-repeat;
}

.visbtn {
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='24' height='24'%3E%3Cpath fill='none' stroke='%23333' d='M2.5 4.5h5v15h-5zM9.5 4.5h5v15h-5zM16.5 4.5h5v15h-5z'/%3E%3C/svg%3E");
  background-position: center;
  background-repeat: no-repeat;
  padding: 15px;
}

#vismenu-content {
  left: 0px;
  font-family: Verdana, sans-serif;
}

.dark .statsbtn,
.dark .savebtn,
.dark .menubtn,
.dark .iobtn,
.dark .visbtn {
  filter: invert(1);
}

.flexbox {
  display: flex;
  align-items: center;
  justify-content: space-between;
  width: 100%;
}

.savebtn {
  background-color: #d6d6d6;
  width: auto;
  height: 30px;
  flex-grow: 1;
  margin: 5px;
  border-radius: 4px;
}

.savebtn:active {
  background-color: #0a0;
  color: white;
}

.dark .savebtn:active {
  /* This will be inverted */
  background-color: #b3b;
}

.stats {
  border-collapse: collapse;
  font-size: 12pt;
  table-layout: fixed;
  width: 100%;
  min-width: 450px;
}

.dark .stats td {
  border: 1px solid #bbb;
}

.stats td {
  border: 1px solid black;
  padding: 5px;
  word-wrap: break-word;
  text-align: center;
  position: relative;
}

#checkbox-stats div {
  position: absolute;
  left: 0;
  top: 0;
  height: 100%;
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
}

#checkbox-stats .bar {
  background-color: rgba(28, 251, 0, 0.6);
}

.menu {
  position: relative;
  display: inline-block;
  margin: 10px 10px 10px 0px;
}

.menu-content {
  font-size: 12pt !important;
  text-align: left !important;
  font-weight: normal !important;
  display: none;
  position: absolute;
  background-color: white;
  right: 0;
  min-width: 300px;
  box-shadow: 0px 8px 16px 0px rgba(0, 0, 0, 0.2);
  z-index: 100;
  padding: 8px;
}

.dark .menu-content {
  background-color: #111;
}

.menu:hover .menu-content {
  display: block;
}

.menu:hover .menubtn,
.menu:hover .iobtn,
.menu:hover .statsbtn {
  background-color: #eee;
}

.menu-label {
  display: inline-block;
  padding: 8px;
  border: 1px solid #ccc;
  border-top: 0;
  width: calc(100% - 18px);
}

.menu-label-top {
  border-top: 1px solid #ccc;
}

.menu-textbox {
  float: left;
  height: 24px;
  margin: 10px 5px;
  padding: 5px 5px;
  font-family: Consolas, "DejaVu Sans Mono", Monaco, monospace;
  font-size: 14px;
  box-sizing: border-box;
  border: 1px solid #888;
  border-radius: 4px;
  outline: none;
  background-color: #eee;
  transition: background-color 0.2s, border 0.2s;
  width: calc(100% - 10px);
}

.menu-textbox.invalid,
.dark .menu-textbox.invalid {
  color: red;
}

.dark .menu-textbox {
  background-color: #222;
  color: #eee;
}

.radio-container {
  margin: 4px;
}

.topmostdiv {
  width: 100%;
  height: 100%;
  background-color: white;
  transition: background-color 0.3s;
}

#top {
  height: 78px;
  border-bottom: 2px solid black;
}

.dark #top {
  border-bottom: 2px solid #ccc;
}

#dbg {
  display: block;
}

::-webkit-scrollbar {
  width: 8px;
}

::-webkit-scrollbar-track {
  background: #aaa;
}

::-webkit-scrollbar-thumb {
  background: #666;
  border-radius: 3px;
}

::-webkit-scrollbar-thumb:hover {
  background: #555;
}

.slider {
  -webkit-appearance: none;
  width: 100%;
  margin: 3px 0;
  padding: 0;
  outline: none;
  opacity: 0.7;
  -webkit-transition: .2s;
  transition: opacity .2s;
  border-radius: 3px;
}

.slider:hover {
  opacity: 1;
}

.slider:focus {
  outline: none;
}

.slider::-webkit-slider-runnable-track {
  -webkit-appearance: none;
  width: 100%;
  height: 8px;
  background: #d3d3d3;
  border-radius: 3px;
  border: none;
}

.slider::-webkit-slider-thumb {
  -webkit-appearance: none;
  width: 15px;
  height: 15px;
  border-radius: 50%;
  background: #0a0;
  cursor: pointer;
  margin-top: -4px;
}

.dark .slider::-webkit-slider-thumb {
  background: #3d3;
}

.slider::-moz-range-thumb {
  width: 15px;
  height: 15px;
  border-radius: 50%;
  background: #0a0;
  cursor: pointer;
}

.slider::-moz-range-track {
  height: 8px;
  background: #d3d3d3;
  border-radius: 3px;
}

.dark .slider::-moz-range-thumb {
  background: #3d3;
}

.slider::-ms-track {
  width: 100%;
  height: 8px;
  border-width: 3px 0;
  background: transparent;
  border-color: transparent;
  color: transparent;
  transition: opacity .2s;
}

.slider::-ms-fill-lower {
  background: #d3d3d3;
  border: none;
  border-radius: 3px;
}

.slider::-ms-fill-upper {
  background: #d3d3d3;
  border: none;
  border-radius: 3px;
}

.slider::-ms-thumb {
  width: 15px;
  height: 15px;
  border-radius: 50%;
  background: #0a0;
  cursor: pointer;
  margin: 0;
}

.shameless-plug {
  font-size: 0.8em;
  text-align: center;
  display: block;
}

a {
  color: #0278a4;
}

.dark a {
  color: #00b9fd;
}

#frontcanvas,
#backcanvas {
  touch-action: none;
}

.placeholder {
  border: 1px dashed #9f9fda !important;
  background-color: #edf2f7 !important;
}

.dragging {
  z-index: 999;
}

.dark .dragging>table>tbody>tr {
  background-color: #252c30;
}

.dark .placeholder {
  filter: invert(1);
}

.column-spacer {
  top: 0;
  left: 0;
  width: calc(100% - 4px);
  position: absolute;
  cursor: pointer;
  user-select: none;
  height: 100%;
}

.column-width-handle {
  top: 0;
  right: 0;
  width: 4px;
  position: absolute;
  cursor: col-resize;
  user-select: none;
  height: 100%;
}

.column-width-handle:hover {
  background-color: #4f99bd;
}

.help-link {
  border: 1px solid #0278a4;
  padding-inline: 0.3rem;
  border-radius: 3px;
  cursor: pointer;
}

.dark .help-link {
  border: 1px solid #00b9fd;
}


  </style>
  <script type="text/javascript" >
///////////////////////////////////////////////
/*
  Split.js - v1.3.5
  MIT License
  https://github.com/nathancahill/Split.js
*/
!function(e,t){"object"==typeof exports&&"undefined"!=typeof module?module.exports=t():"function"==typeof define&&define.amd?define(t):e.Split=t()}(this,function(){"use strict";var e=window,t=e.document,n="addEventListener",i="removeEventListener",r="getBoundingClientRect",s=function(){return!1},o=e.attachEvent&&!e[n],a=["","-webkit-","-moz-","-o-"].filter(function(e){var n=t.createElement("div");return n.style.cssText="width:"+e+"calc(9px)",!!n.style.length}).shift()+"calc",l=function(e){return"string"==typeof e||e instanceof String?t.querySelector(e):e};return function(u,c){function z(e,t,n){var i=A(y,t,n);Object.keys(i).forEach(function(t){return e.style[t]=i[t]})}function h(e,t){var n=B(y,t);Object.keys(n).forEach(function(t){return e.style[t]=n[t]})}function f(e){var t=E[this.a],n=E[this.b],i=t.size+n.size;t.size=e/this.size*i,n.size=i-e/this.size*i,z(t.element,t.size,this.aGutterSize),z(n.element,n.size,this.bGutterSize)}function m(e){var t;this.dragging&&((t="touches"in e?e.touches[0][b]-this.start:e[b]-this.start)<=E[this.a].minSize+M+this.aGutterSize?t=E[this.a].minSize+this.aGutterSize:t>=this.size-(E[this.b].minSize+M+this.bGutterSize)&&(t=this.size-(E[this.b].minSize+this.bGutterSize)),f.call(this,t),c.onDrag&&c.onDrag())}function g(){var e=E[this.a].element,t=E[this.b].element;this.size=e[r]()[y]+t[r]()[y]+this.aGutterSize+this.bGutterSize,this.start=e[r]()[G]}function d(){var t=this,n=E[t.a].element,r=E[t.b].element;t.dragging&&c.onDragEnd&&c.onDragEnd(),t.dragging=!1,e[i]("mouseup",t.stop),e[i]("touchend",t.stop),e[i]("touchcancel",t.stop),t.parent[i]("mousemove",t.move),t.parent[i]("touchmove",t.move),delete t.stop,delete t.move,n[i]("selectstart",s),n[i]("dragstart",s),r[i]("selectstart",s),r[i]("dragstart",s),n.style.userSelect="",n.style.webkitUserSelect="",n.style.MozUserSelect="",n.style.pointerEvents="",r.style.userSelect="",r.style.webkitUserSelect="",r.style.MozUserSelect="",r.style.pointerEvents="",t.gutter.style.cursor="",t.parent.style.cursor=""}function S(t){var i=this,r=E[i.a].element,o=E[i.b].element;!i.dragging&&c.onDragStart&&c.onDragStart(),t.preventDefault(),i.dragging=!0,i.move=m.bind(i),i.stop=d.bind(i),e[n]("mouseup",i.stop),e[n]("touchend",i.stop),e[n]("touchcancel",i.stop),i.parent[n]("mousemove",i.move),i.parent[n]("touchmove",i.move),r[n]("selectstart",s),r[n]("dragstart",s),o[n]("selectstart",s),o[n]("dragstart",s),r.style.userSelect="none",r.style.webkitUserSelect="none",r.style.MozUserSelect="none",r.style.pointerEvents="none",o.style.userSelect="none",o.style.webkitUserSelect="none",o.style.MozUserSelect="none",o.style.pointerEvents="none",i.gutter.style.cursor=j,i.parent.style.cursor=j,g.call(i)}function v(e){e.forEach(function(t,n){if(n>0){var i=F[n-1],r=E[i.a],s=E[i.b];r.size=e[n-1],s.size=t,z(r.element,r.size,i.aGutterSize),z(s.element,s.size,i.bGutterSize)}})}function p(){F.forEach(function(e){e.parent.removeChild(e.gutter),E[e.a].element.style[y]="",E[e.b].element.style[y]=""})}void 0===c&&(c={});var y,b,G,E,w=l(u[0]).parentNode,D=e.getComputedStyle(w).flexDirection,U=c.sizes||u.map(function(){return 100/u.length}),k=void 0!==c.minSize?c.minSize:100,x=Array.isArray(k)?k:u.map(function(){return k}),L=void 0!==c.gutterSize?c.gutterSize:10,M=void 0!==c.snapOffset?c.snapOffset:30,O=c.direction||"horizontal",j=c.cursor||("horizontal"===O?"ew-resize":"ns-resize"),C=c.gutter||function(e,n){var i=t.createElement("div");return i.className="gutter gutter-"+n,i},A=c.elementStyle||function(e,t,n){var i={};return"string"==typeof t||t instanceof String?i[e]=t:i[e]=o?t+"%":a+"("+t+"% - "+n+"px)",i},B=c.gutterStyle||function(e,t){return n={},n[e]=t+"px",n;var n};"horizontal"===O?(y="width","clientWidth",b="clientX",G="left","paddingLeft"):"vertical"===O&&(y="height","clientHeight",b="clientY",G="top","paddingTop");var F=[];return E=u.map(function(e,t){var i,s={element:l(e),size:U[t],minSize:x[t]};if(t>0&&(i={a:t-1,b:t,dragging:!1,isFirst:1===t,isLast:t===u.length-1,direction:O,parent:w},i.aGutterSize=L,i.bGutterSize=L,i.isFirst&&(i.aGutterSize=L/2),i.isLast&&(i.bGutterSize=L/2),"row-reverse"===D||"column-reverse"===D)){var a=i.a;i.a=i.b,i.b=a}if(!o&&t>0){var c=C(t,O);h(c,L),c[n]("mousedown",S.bind(i)),c[n]("touchstart",S.bind(i)),w.insertBefore(c,s.element),i.gutter=c}0===t||t===u.length-1?z(s.element,s.size,L/2):z(s.element,s.size,L);var f=s.element[r]()[y];return f<s.minSize&&(s.minSize=f),t>0&&F.push(i),s}),o?{setSizes:v,destroy:p}:{setSizes:v,getSizes:function(){return E.map(function(e){return e.size})},collapse:function(e){if(e===F.length){var t=F[e-1];g.call(t),o||f.call(t,t.size-t.bGutterSize)}else{var n=F[e];g.call(n),o||f.call(n,n.aGutterSize)}},destroy:p}}});

///////////////////////////////////////////////

///////////////////////////////////////////////
// Copyright (c) 2013 Pieroxy <pieroxy@pieroxy.net>
// This work is free. You can redistribute it and/or modify it
// under the terms of the WTFPL, Version 2
// For more information see LICENSE.txt or http://www.wtfpl.net/
//
// For more information, the home page:
// http://pieroxy.net/blog/pages/lz-string/testing.html
//
// LZ-based compression algorithm, version 1.4.4
var LZString=function(){var o=String.fromCharCode,i={};var n={decompressFromBase64:function(o){return null==o?"":""==o?null:n._decompress(o.length,32,function(n){return function(o,n){if(!i[o]){i[o]={};for(var t=0;t<o.length;t++)i[o][o.charAt(t)]=t}return i[o][n]}("ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/=",o.charAt(n))})},_decompress:function(i,n,t){var r,e,a,s,p,u,l,f=[],c=4,d=4,h=3,v="",g=[],m={val:t(0),position:n,index:1};for(r=0;r<3;r+=1)f[r]=r;for(a=0,p=Math.pow(2,2),u=1;u!=p;)s=m.val&m.position,m.position>>=1,0==m.position&&(m.position=n,m.val=t(m.index++)),a|=(s>0?1:0)*u,u<<=1;switch(a){case 0:for(a=0,p=Math.pow(2,8),u=1;u!=p;)s=m.val&m.position,m.position>>=1,0==m.position&&(m.position=n,m.val=t(m.index++)),a|=(s>0?1:0)*u,u<<=1;l=o(a);break;case 1:for(a=0,p=Math.pow(2,16),u=1;u!=p;)s=m.val&m.position,m.position>>=1,0==m.position&&(m.position=n,m.val=t(m.index++)),a|=(s>0?1:0)*u,u<<=1;l=o(a);break;case 2:return""}for(f[3]=l,e=l,g.push(l);;){if(m.index>i)return"";for(a=0,p=Math.pow(2,h),u=1;u!=p;)s=m.val&m.position,m.position>>=1,0==m.position&&(m.position=n,m.val=t(m.index++)),a|=(s>0?1:0)*u,u<<=1;switch(l=a){case 0:for(a=0,p=Math.pow(2,8),u=1;u!=p;)s=m.val&m.position,m.position>>=1,0==m.position&&(m.position=n,m.val=t(m.index++)),a|=(s>0?1:0)*u,u<<=1;f[d++]=o(a),l=d-1,c--;break;case 1:for(a=0,p=Math.pow(2,16),u=1;u!=p;)s=m.val&m.position,m.position>>=1,0==m.position&&(m.position=n,m.val=t(m.index++)),a|=(s>0?1:0)*u,u<<=1;f[d++]=o(a),l=d-1,c--;break;case 2:return g.join("")}if(0==c&&(c=Math.pow(2,h),h++),f[l])v=f[l];else{if(l!==d)return null;v=e+e.charAt(0)}g.push(v),f[d++]=e+v.charAt(0),e=v,0==--c&&(c=Math.pow(2,h),h++)}}};return n}();"function"==typeof define&&define.amd?define(function(){return LZString}):"undefined"!=typeof module&&null!=module?module.exports=LZString:"undefined"!=typeof angular&&null!=angular&&angular.module("LZString",[]).factory("LZString",function(){return LZString});
///////////////////////////////////////////////

///////////////////////////////////////////////
/*!
 * PEP v0.4.3 | https://github.com/jquery/PEP
 * Copyright jQuery Foundation and other contributors | http://jquery.org/license
 */
!function(a,b){"object"==typeof exports&&"undefined"!=typeof module?module.exports=b():"function"==typeof define&&define.amd?define(b):a.PointerEventsPolyfill=b()}(this,function(){"use strict";function a(a,b){b=b||Object.create(null);var c=document.createEvent("Event");c.initEvent(a,b.bubbles||!1,b.cancelable||!1);
for(var d,e=2;e<m.length;e++)d=m[e],c[d]=b[d]||n[e];c.buttons=b.buttons||0;
var f=0;return f=b.pressure&&c.buttons?b.pressure:c.buttons?.5:0,c.x=c.clientX,c.y=c.clientY,c.pointerId=b.pointerId||0,c.width=b.width||0,c.height=b.height||0,c.pressure=f,c.tiltX=b.tiltX||0,c.tiltY=b.tiltY||0,c.twist=b.twist||0,c.tangentialPressure=b.tangentialPressure||0,c.pointerType=b.pointerType||"",c.hwTimestamp=b.hwTimestamp||0,c.isPrimary=b.isPrimary||!1,c}function b(){this.array=[],this.size=0}function c(a,b,c,d){this.addCallback=a.bind(d),this.removeCallback=b.bind(d),this.changedCallback=c.bind(d),A&&(this.observer=new A(this.mutationWatcher.bind(this)))}function d(a){return"body /shadow-deep/ "+e(a)}function e(a){return'[touch-action="'+a+'"]'}function f(a){return"{ -ms-touch-action: "+a+"; touch-action: "+a+"; }"}function g(){if(F){D.forEach(function(a){String(a)===a?(E+=e(a)+f(a)+"\n",G&&(E+=d(a)+f(a)+"\n")):(E+=a.selectors.map(e)+f(a.rule)+"\n",G&&(E+=a.selectors.map(d)+f(a.rule)+"\n"))});var a=document.createElement("style");a.textContent=E,document.head.appendChild(a)}}function h(){if(!window.PointerEvent){if(window.PointerEvent=a,window.navigator.msPointerEnabled){var b=window.navigator.msMaxTouchPoints;Object.defineProperty(window.navigator,"maxTouchPoints",{value:b,enumerable:!0}),u.registerSource("ms",_)}else Object.defineProperty(window.navigator,"maxTouchPoints",{value:0,enumerable:!0}),u.registerSource("mouse",N),void 0!==window.ontouchstart&&u.registerSource("touch",V);u.register(document)}}function i(a){if(!u.pointermap.has(a)){var b=new Error("InvalidPointerId");throw b.name="InvalidPointerId",b}}function j(a){for(var b=a.parentNode;b&&b!==a.ownerDocument;)b=b.parentNode;if(!b){var c=new Error("InvalidStateError");throw c.name="InvalidStateError",c}}function k(a){var b=u.pointermap.get(a);return 0!==b.buttons}function l(){window.Element&&!Element.prototype.setPointerCapture&&Object.defineProperties(Element.prototype,{setPointerCapture:{value:W},releasePointerCapture:{value:X},hasPointerCapture:{value:Y}})}
var m=["bubbles","cancelable","view","detail","screenX","screenY","clientX","clientY","ctrlKey","altKey","shiftKey","metaKey","button","relatedTarget","pageX","pageY"],n=[!1,!1,null,null,0,0,0,0,!1,!1,!1,!1,0,null,0,0],o=window.Map&&window.Map.prototype.forEach,p=o?Map:b;b.prototype={set:function(a,b){return void 0===b?this["delete"](a):(this.has(a)||this.size++,void(this.array[a]=b))},has:function(a){return void 0!==this.array[a]},"delete":function(a){this.has(a)&&(delete this.array[a],this.size--)},get:function(a){return this.array[a]},clear:function(){this.array.length=0,this.size=0},forEach:function(a,b){return this.array.forEach(function(c,d){a.call(b,c,d,this)},this)}};var q=["bubbles","cancelable","view","detail","screenX","screenY","clientX","clientY","ctrlKey","altKey","shiftKey","metaKey","button","relatedTarget","buttons","pointerId","width","height","pressure","tiltX","tiltY","pointerType","hwTimestamp","isPrimary","type","target","currentTarget","which","pageX","pageY","timeStamp"],r=[!1,!1,null,null,0,0,0,0,!1,!1,!1,!1,0,null,0,0,0,0,0,0,0,"",0,!1,"",null,null,0,0,0,0],s={pointerover:1,pointerout:1,pointerenter:1,pointerleave:1},t="undefined"!=typeof SVGElementInstance,u={pointermap:new p,eventMap:Object.create(null),captureInfo:Object.create(null),eventSources:Object.create(null),eventSourceList:[],registerSource:function(a,b){var c=b,d=c.events;d&&(d.forEach(function(a){c[a]&&(this.eventMap[a]=c[a].bind(c))},this),this.eventSources[a]=c,this.eventSourceList.push(c))},register:function(a){for(var b,c=this.eventSourceList.length,d=0;d<c&&(b=this.eventSourceList[d]);d++)
b.register.call(b,a)},unregister:function(a){for(var b,c=this.eventSourceList.length,d=0;d<c&&(b=this.eventSourceList[d]);d++)
b.unregister.call(b,a)},contains:function(a,b){try{return a.contains(b)}catch(c){return!1}},down:function(a){a.bubbles=!0,this.fireEvent("pointerdown",a)},move:function(a){a.bubbles=!0,this.fireEvent("pointermove",a)},up:function(a){a.bubbles=!0,this.fireEvent("pointerup",a)},enter:function(a){a.bubbles=!1,this.fireEvent("pointerenter",a)},leave:function(a){a.bubbles=!1,this.fireEvent("pointerleave",a)},over:function(a){a.bubbles=!0,this.fireEvent("pointerover",a)},out:function(a){a.bubbles=!0,this.fireEvent("pointerout",a)},cancel:function(a){a.bubbles=!0,this.fireEvent("pointercancel",a)},leaveOut:function(a){this.out(a),this.propagate(a,this.leave,!1)},enterOver:function(a){this.over(a),this.propagate(a,this.enter,!0)},eventHandler:function(a){if(!a._handledByPE){var b=a.type,c=this.eventMap&&this.eventMap[b];c&&c(a),a._handledByPE=!0}},listen:function(a,b){b.forEach(function(b){this.addEvent(a,b)},this)},unlisten:function(a,b){b.forEach(function(b){this.removeEvent(a,b)},this)},addEvent:function(a,b){a.addEventListener(b,this.boundHandler)},removeEvent:function(a,b){a.removeEventListener(b,this.boundHandler)},makeEvent:function(b,c){this.captureInfo[c.pointerId]&&(c.relatedTarget=null);var d=new a(b,c);return c.preventDefault&&(d.preventDefault=c.preventDefault),d._target=d._target||c.target,d},fireEvent:function(a,b){var c=this.makeEvent(a,b);return this.dispatchEvent(c)},cloneEvent:function(a){for(var b,c=Object.create(null),d=0;d<q.length;d++)b=q[d],c[b]=a[b]||r[d],!t||"target"!==b&&"relatedTarget"!==b||c[b]instanceof SVGElementInstance&&(c[b]=c[b].correspondingUseElement);return a.preventDefault&&(c.preventDefault=function(){a.preventDefault()}),c},getTarget:function(a){var b=this.captureInfo[a.pointerId];return b?a._target!==b&&a.type in s?void 0:b:a._target},propagate:function(a,b,c){for(var d=a.target,e=[];d!==document&&!d.contains(a.relatedTarget);) if(e.push(d),d=d.parentNode,!d)return;c&&e.reverse(),e.forEach(function(c){a.target=c,b.call(this,a)},this)},setCapture:function(b,c,d){this.captureInfo[b]&&this.releaseCapture(b,d),this.captureInfo[b]=c,this.implicitRelease=this.releaseCapture.bind(this,b,d),document.addEventListener("pointerup",this.implicitRelease),document.addEventListener("pointercancel",this.implicitRelease);var e=new a("gotpointercapture");e.pointerId=b,e._target=c,d||this.asyncDispatchEvent(e)},releaseCapture:function(b,c){var d=this.captureInfo[b];if(d){this.captureInfo[b]=void 0,document.removeEventListener("pointerup",this.implicitRelease),document.removeEventListener("pointercancel",this.implicitRelease);var e=new a("lostpointercapture");e.pointerId=b,e._target=d,c||this.asyncDispatchEvent(e)}},dispatchEvent:/*scope.external.dispatchEvent || */function(a){var b=this.getTarget(a);if(b)return b.dispatchEvent(a)},asyncDispatchEvent:function(a){requestAnimationFrame(this.dispatchEvent.bind(this,a))}};u.boundHandler=u.eventHandler.bind(u);var v={shadow:function(a){if(a)return a.shadowRoot||a.webkitShadowRoot},canTarget:function(a){return a&&Boolean(a.elementFromPoint)},targetingShadow:function(a){var b=this.shadow(a);if(this.canTarget(b))return b},olderShadow:function(a){var b=a.olderShadowRoot;if(!b){var c=a.querySelector("shadow");c&&(b=c.olderShadowRoot)}return b},allShadows:function(a){for(var b=[],c=this.shadow(a);c;)b.push(c),c=this.olderShadow(c);return b},searchRoot:function(a,b,c){if(a){var d,e,f=a.elementFromPoint(b,c);for(e=this.targetingShadow(f);e;){if(d=e.elementFromPoint(b,c)){var g=this.targetingShadow(d);return this.searchRoot(g,b,c)||d} e=this.olderShadow(e)} return f}},owner:function(a){
for(var b=a;b.parentNode;)b=b.parentNode;
return b.nodeType!==Node.DOCUMENT_NODE&&b.nodeType!==Node.DOCUMENT_FRAGMENT_NODE&&(b=document),b},findTarget:function(a){var b=a.clientX,c=a.clientY,d=this.owner(a.target);
return d.elementFromPoint(b,c)||(d=document),this.searchRoot(d,b,c)}},w=Array.prototype.forEach.call.bind(Array.prototype.forEach),x=Array.prototype.map.call.bind(Array.prototype.map),y=Array.prototype.slice.call.bind(Array.prototype.slice),z=Array.prototype.filter.call.bind(Array.prototype.filter),A=window.MutationObserver||window.WebKitMutationObserver,B="[touch-action]",C={subtree:!0,childList:!0,attributes:!0,attributeOldValue:!0,attributeFilter:["touch-action"]};c.prototype={watchSubtree:function(a){
//
this.observer&&v.canTarget(a)&&this.observer.observe(a,C)},enableOnSubtree:function(a){this.watchSubtree(a),a===document&&"complete"!==document.readyState?this.installOnLoad():this.installNewSubtree(a)},installNewSubtree:function(a){w(this.findElements(a),this.addElement,this)},findElements:function(a){return a.querySelectorAll?a.querySelectorAll(B):[]},removeElement:function(a){this.removeCallback(a)},addElement:function(a){this.addCallback(a)},elementChanged:function(a,b){this.changedCallback(a,b)},concatLists:function(a,b){return a.concat(y(b))},
installOnLoad:function(){document.addEventListener("readystatechange",function(){"complete"===document.readyState&&this.installNewSubtree(document)}.bind(this))},isElement:function(a){return a.nodeType===Node.ELEMENT_NODE},flattenMutationTree:function(a){
var b=x(a,this.findElements,this);
return b.push(z(a,this.isElement)),b.reduce(this.concatLists,[])},mutationWatcher:function(a){a.forEach(this.mutationHandler,this)},mutationHandler:function(a){if("childList"===a.type){var b=this.flattenMutationTree(a.addedNodes);b.forEach(this.addElement,this);var c=this.flattenMutationTree(a.removedNodes);c.forEach(this.removeElement,this)}else"attributes"===a.type&&this.elementChanged(a.target,a.oldValue)}};var D=["none","auto","pan-x","pan-y",{rule:"pan-x pan-y",selectors:["pan-x pan-y","pan-y pan-x"]}],E="",F=window.PointerEvent||window.MSPointerEvent,G=!window.ShadowDOMPolyfill&&document.head.createShadowRoot,H=u.pointermap,I=25,J=[1,4,2,8,16],K=!1;try{K=1===new MouseEvent("test",{buttons:1}).buttons}catch(L){}
var M,N={POINTER_ID:1,POINTER_TYPE:"mouse",events:["mousedown","mousemove","mouseup","mouseover","mouseout"],register:function(a){u.listen(a,this.events)},unregister:function(a){u.unlisten(a,this.events)},lastTouches:[],
isEventSimulatedFromTouch:function(a){for(var b,c=this.lastTouches,d=a.clientX,e=a.clientY,f=0,g=c.length;f<g&&(b=c[f]);f++){
var h=Math.abs(d-b.x),i=Math.abs(e-b.y);if(h<=I&&i<=I)return!0}},prepareEvent:function(a){var b=u.cloneEvent(a),c=b.preventDefault;return b.preventDefault=function(){a.preventDefault(),c()},b.pointerId=this.POINTER_ID,b.isPrimary=!0,b.pointerType=this.POINTER_TYPE,b},prepareButtonsForMove:function(a,b){var c=H.get(this.POINTER_ID);
0!==b.which&&c?a.buttons=c.buttons:a.buttons=0,b.buttons=a.buttons},mousedown:function(a){if(!this.isEventSimulatedFromTouch(a)){var b=H.get(this.POINTER_ID),c=this.prepareEvent(a);K||(c.buttons=J[c.button],b&&(c.buttons|=b.buttons),a.buttons=c.buttons),H.set(this.POINTER_ID,a),b&&0!==b.buttons?u.move(c):u.down(c)}},mousemove:function(a){if(!this.isEventSimulatedFromTouch(a)){var b=this.prepareEvent(a);K||this.prepareButtonsForMove(b,a),b.button=-1,H.set(this.POINTER_ID,a),u.move(b)}},mouseup:function(a){if(!this.isEventSimulatedFromTouch(a)){var b=H.get(this.POINTER_ID),c=this.prepareEvent(a);if(!K){var d=J[c.button];
c.buttons=b?b.buttons&~d:0,a.buttons=c.buttons}H.set(this.POINTER_ID,a),
c.buttons&=~J[c.button],0===c.buttons?u.up(c):u.move(c)}},mouseover:function(a){if(!this.isEventSimulatedFromTouch(a)){var b=this.prepareEvent(a);K||this.prepareButtonsForMove(b,a),b.button=-1,H.set(this.POINTER_ID,a),u.enterOver(b)}},mouseout:function(a){if(!this.isEventSimulatedFromTouch(a)){var b=this.prepareEvent(a);K||this.prepareButtonsForMove(b,a),b.button=-1,u.leaveOut(b)}},cancel:function(a){var b=this.prepareEvent(a);u.cancel(b),this.deactivateMouse()},deactivateMouse:function(){H["delete"](this.POINTER_ID)}},O=u.captureInfo,P=v.findTarget.bind(v),Q=v.allShadows.bind(v),R=u.pointermap,S=2500,T=200,U="touch-action",V={events:["touchstart","touchmove","touchend","touchcancel"],register:function(a){M.enableOnSubtree(a)},unregister:function(){},elementAdded:function(a){var b=a.getAttribute(U),c=this.touchActionToScrollType(b);c&&(a._scrollType=c,u.listen(a,this.events),
Q(a).forEach(function(a){a._scrollType=c,u.listen(a,this.events)},this))},elementRemoved:function(a){a._scrollType=void 0,u.unlisten(a,this.events),
Q(a).forEach(function(a){a._scrollType=void 0,u.unlisten(a,this.events)},this)},elementChanged:function(a,b){var c=a.getAttribute(U),d=this.touchActionToScrollType(c),e=this.touchActionToScrollType(b);
d&&e?(a._scrollType=d,Q(a).forEach(function(a){a._scrollType=d},this)):e?this.elementRemoved(a):d&&this.elementAdded(a)},scrollTypes:{EMITTER:"none",XSCROLLER:"pan-x",YSCROLLER:"pan-y",SCROLLER:/^(?:pan-x pan-y)|(?:pan-y pan-x)|auto$/},touchActionToScrollType:function(a){var b=a,c=this.scrollTypes;return"none"===b?"none":b===c.XSCROLLER?"X":b===c.YSCROLLER?"Y":c.SCROLLER.exec(b)?"XY":void 0},POINTER_TYPE:"touch",firstTouch:null,isPrimaryTouch:function(a){return this.firstTouch===a.identifier},setPrimaryTouch:function(a){
(0===R.size||1===R.size&&R.has(1))&&(this.firstTouch=a.identifier,this.firstXY={X:a.clientX,Y:a.clientY},this.scrolling=!1,this.cancelResetClickCount())},removePrimaryPointer:function(a){a.isPrimary&&(this.firstTouch=null,this.firstXY=null,this.resetClickCount())},clickCount:0,resetId:null,resetClickCount:function(){var a=function(){this.clickCount=0,this.resetId=null}.bind(this);this.resetId=setTimeout(a,T)},cancelResetClickCount:function(){this.resetId&&clearTimeout(this.resetId)},typeToButtons:function(a){var b=0;return"touchstart"!==a&&"touchmove"!==a||(b=1),b},touchToPointer:function(a){var b=this.currentTouchEvent,c=u.cloneEvent(a),d=c.pointerId=a.identifier+2;c.target=O[d]||P(c),c.bubbles=!0,c.cancelable=!0,c.detail=this.clickCount,c.button=0,c.buttons=this.typeToButtons(b.type),c.width=2*(a.radiusX||a.webkitRadiusX||0),c.height=2*(a.radiusY||a.webkitRadiusY||0),c.pressure=a.force||a.webkitForce||.5,c.isPrimary=this.isPrimaryTouch(a),c.pointerType=this.POINTER_TYPE,
c.altKey=b.altKey,c.ctrlKey=b.ctrlKey,c.metaKey=b.metaKey,c.shiftKey=b.shiftKey;
var e=this;return c.preventDefault=function(){e.scrolling=!1,e.firstXY=null,b.preventDefault()},c},processTouches:function(a,b){var c=a.changedTouches;this.currentTouchEvent=a;for(var d,e=0;e<c.length;e++)d=c[e],b.call(this,this.touchToPointer(d))},
shouldScroll:function(a){if(this.firstXY){var b,c=a.currentTarget._scrollType;if("none"===c)
b=!1;else if("XY"===c)
b=!0;else{var d=a.changedTouches[0],e=c,f="Y"===c?"X":"Y",g=Math.abs(d["client"+e]-this.firstXY[e]),h=Math.abs(d["client"+f]-this.firstXY[f]);
b=g>=h}return this.firstXY=null,b}},findTouch:function(a,b){for(var c,d=0,e=a.length;d<e&&(c=a[d]);d++)if(c.identifier===b)return!0},
vacuumTouches:function(a){var b=a.touches;
if(R.size>=b.length){var c=[];R.forEach(function(a,d){
if(1!==d&&!this.findTouch(b,d-2)){var e=a.out;c.push(e)}},this),c.forEach(this.cancelOut,this)}},touchstart:function(a){this.vacuumTouches(a),this.setPrimaryTouch(a.changedTouches[0]),this.dedupSynthMouse(a),this.scrolling||(this.clickCount++,this.processTouches(a,this.overDown))},overDown:function(a){R.set(a.pointerId,{target:a.target,out:a,outTarget:a.target}),u.enterOver(a),u.down(a)},touchmove:function(a){this.scrolling||(this.shouldScroll(a)?(this.scrolling=!0,this.touchcancel(a)):(a.preventDefault(),this.processTouches(a,this.moveOverOut)))},moveOverOut:function(a){var b=a,c=R.get(b.pointerId);
if(c){var d=c.out,e=c.outTarget;u.move(b),d&&e!==b.target&&(d.relatedTarget=b.target,b.relatedTarget=e,
d.target=e,b.target?(u.leaveOut(d),u.enterOver(b)):(
b.target=e,b.relatedTarget=null,this.cancelOut(b))),c.out=b,c.outTarget=b.target}},touchend:function(a){this.dedupSynthMouse(a),this.processTouches(a,this.upOut)},upOut:function(a){this.scrolling||(u.up(a),u.leaveOut(a)),this.cleanUpPointer(a)},touchcancel:function(a){this.processTouches(a,this.cancelOut)},cancelOut:function(a){u.cancel(a),u.leaveOut(a),this.cleanUpPointer(a)},cleanUpPointer:function(a){R["delete"](a.pointerId),this.removePrimaryPointer(a)},
dedupSynthMouse:function(a){var b=N.lastTouches,c=a.changedTouches[0];
if(this.isPrimaryTouch(c)){
var d={x:c.clientX,y:c.clientY};b.push(d);var e=function(a,b){var c=a.indexOf(b);c>-1&&a.splice(c,1)}.bind(null,b,d);setTimeout(e,S)}}};M=new c(V.elementAdded,V.elementRemoved,V.elementChanged,V);var W,X,Y,Z=u.pointermap,$=window.MSPointerEvent&&"number"==typeof window.MSPointerEvent.MSPOINTER_TYPE_MOUSE,_={events:["MSPointerDown","MSPointerMove","MSPointerUp","MSPointerOut","MSPointerOver","MSPointerCancel","MSGotPointerCapture","MSLostPointerCapture"],register:function(a){u.listen(a,this.events)},unregister:function(a){u.unlisten(a,this.events)},POINTER_TYPES:["","unavailable","touch","pen","mouse"],prepareEvent:function(a){var b=a;return $&&(b=u.cloneEvent(a),b.pointerType=this.POINTER_TYPES[a.pointerType]),b},cleanup:function(a){Z["delete"](a)},MSPointerDown:function(a){Z.set(a.pointerId,a);var b=this.prepareEvent(a);u.down(b)},MSPointerMove:function(a){var b=this.prepareEvent(a);u.move(b)},MSPointerUp:function(a){var b=this.prepareEvent(a);u.up(b),this.cleanup(a.pointerId)},MSPointerOut:function(a){var b=this.prepareEvent(a);u.leaveOut(b)},MSPointerOver:function(a){var b=this.prepareEvent(a);u.enterOver(b)},MSPointerCancel:function(a){var b=this.prepareEvent(a);u.cancel(b),this.cleanup(a.pointerId)},MSLostPointerCapture:function(a){var b=u.makeEvent("lostpointercapture",a);u.dispatchEvent(b)},MSGotPointerCapture:function(a){var b=u.makeEvent("gotpointercapture",a);u.dispatchEvent(b)}},aa=window.navigator;aa.msPointerEnabled?(W=function(a){i(a),j(this),k(a)&&(u.setCapture(a,this,!0),this.msSetPointerCapture(a))},X=function(a){i(a),u.releaseCapture(a,!0),this.msReleasePointerCapture(a)}):(W=function(a){i(a),j(this),k(a)&&u.setCapture(a,this)},X=function(a){i(a),u.releaseCapture(a)}),Y=function(a){return!!u.captureInfo[a]},g(),h(),l();var ba={dispatcher:u,Installer:c,PointerEvent:a,PointerMap:p,targetFinding:v};return ba});

///////////////////////////////////////////////

///////////////////////////////////////////////
var config = {"dark_mode": false, "show_pads": true, "show_fabrication": false, "show_silkscreen": true, "highlight_pin1": false, "redraw_on_drag": true, "board_rotation": 0, "checkboxes": "Sourced,Placed", "bom_view": "left-right", "layer_view": "FB", "fields": ["Value", "Footprint"]}
///////////////////////////////////////////////

///////////////////////////////////////////////
var pcbdata = JSON.parse(LZString.decompressFromBase64("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FybJAfJpHLWClQtiaYmqJviauqJJpRY3QVJvNABmiABya8mgpuKbagMprGAKmnEt+BQyyZqibpmuJoSb5mkcEWaDANJpWa1mkenyaimkpu2bdmkcuOVDm6Js0BYm2Zq8AzmlJsublmrJtWbeZEZu/A7mzZtKbymyps0A/glQoABqKEFhbfgGytebjmz5sSbkmi5qub/mm5uBaNmh5vBa9mzQH8KkW95pmbTmtFqWb0mzFsBb1m+5q2a8WkctzyiWgkpJa5mslt+aKW7JqpbbmnFtpadmiFsYAvAX/LEwoQIVqqbqm3wqObiWk5pZaFm8luubOW7FppawW3lvxb+WiZpIq6mogAaammlpoya2mzQE6anAHpr6aVmoZskARmiQDGaqm3usZbxWqVq+bWWjFo5b0wIFpoAQW3FuVb/8hPONAByERqjrsAcRujBRqjgEMaZG4QDkbowUMoYBFGwkruBVGtmpcbu8LRruBdGvwruA3iXwtzzEsBxujobG68osarGxxtzasalxpMbC25xuaBNG9xr8BPGxgCgN3ChPIyQqMfptoboGtAwTyCAPhvgB7QEfKIbqMAYHtB+ISQCfggAA"))
///////////////////////////////////////////////

///////////////////////////////////////////////
/* Utility functions */

var storagePrefix = 'KiCad_HTML_BOM__' + pcbdata.metadata.title + '__' +
  pcbdata.metadata.revision + '__#';
var storage;

function initStorage(key) {
  try {
    window.localStorage.getItem("blank");
    storage = window.localStorage;
  } catch (e) {
    // localStorage not available
  }
  if (!storage) {
    try {
      window.sessionStorage.getItem("blank");
      storage = window.sessionStorage;
    } catch (e) {
      // sessionStorage also not available
    }
  }
}

function readStorage(key) {
  if (storage) {
    return storage.getItem(storagePrefix + key);
  } else {
    return null;
  }
}

function writeStorage(key, value) {
  if (storage) {
    storage.setItem(storagePrefix + key, value);
  }
}

function fancyDblClickHandler(el, onsingle, ondouble) {
  return function() {
    if (el.getAttribute("data-dblclick") == null) {
      el.setAttribute("data-dblclick", 1);
      setTimeout(function() {
        if (el.getAttribute("data-dblclick") == 1) {
          onsingle();
        }
        el.removeAttribute("data-dblclick");
      }, 200);
    } else {
      el.removeAttribute("data-dblclick");
      ondouble();
    }
  }
}

function smoothScrollToRow(rowid) {
  document.getElementById(rowid).scrollIntoView({
    behavior: "smooth",
    block: "center",
    inline: "nearest"
  });
}

function focusInputField(input) {
  input.scrollIntoView(false);
  input.focus();
  input.select();
}

function saveBomTable(output) {
  var text = '';
  for (var node of bomhead.childNodes[0].childNodes) {
    if (node.firstChild) {
      text += (output == 'csv' ? `"${node.firstChild.nodeValue}"` : node.firstChild.nodeValue);
    }
    if (node != bomhead.childNodes[0].lastChild) {
      text += (output == 'csv' ? ',' : '\t');
    }
  }
  text += '\n';
  for (var row of bombody.childNodes) {
    for (var cell of row.childNodes) {
      let val = '';
      for (var node of cell.childNodes) {
        if (node.nodeName == "INPUT") {
          if (node.checked) {
            val += '✓';
          }
        } else if (node.nodeName == "MARK") {
          val += node.firstChild.nodeValue;
        } else {
          val += node.nodeValue;
        }
      }
      if (output == 'csv') {
        val = val.replace(/\"/g, '\"\"'); // pair of double-quote characters
        if (isNumeric(val)) {
          val = +val;                     // use number
        } else {
          val = `"${val}"`;               // enclosed within double-quote
        }
      }
      text += val;
      if (cell != row.lastChild) {
        text += (output == 'csv' ? ',' : '\t');
      }
    }
    text += '\n';
  }

  if (output != 'clipboard') {
    // To file: csv or txt
    var blob = new Blob([text], {
      type: `text/${output}`
    });
    saveFile(`${pcbdata.metadata.title}.${output}`, blob);
  } else {
    // To clipboard
    var textArea = document.createElement("textarea");
    textArea.classList.add('clipboard-temp');
    textArea.value = text;

    document.body.appendChild(textArea);
    textArea.focus();
    textArea.select();

    try {
      if (document.execCommand('copy')) {
        console.log('Bom copied to clipboard.');
      }
    } catch (err) {
      console.log('Can not copy to clipboard.');
    }

    document.body.removeChild(textArea);
  }
}

function isNumeric(str) {
  /* https://stackoverflow.com/a/175787 */
  return (typeof str != "string" ? false : !isNaN(str) && !isNaN(parseFloat(str)));
}

function removeGutterNode(node) {
  for (var i = 0; i < node.childNodes.length; i++) {
    if (node.childNodes[i].classList &&
      node.childNodes[i].classList.contains("gutter")) {
      node.removeChild(node.childNodes[i]);
      break;
    }
  }
}

function cleanGutters() {
  removeGutterNode(document.getElementById("bot"));
  removeGutterNode(document.getElementById("canvasdiv"));
}

var units = {
  prefixes: {
    giga: ["G", "g", "giga", "Giga", "GIGA"],
    mega: ["M", "mega", "Mega", "MEGA"],
    kilo: ["K", "k", "kilo", "Kilo", "KILO"],
    milli: ["m", "milli", "Milli", "MILLI"],
    micro: ["U", "u", "micro", "Micro", "MICRO", "μ", "µ"], // different utf8 μ
    nano: ["N", "n", "nano", "Nano", "NANO"],
    pico: ["P", "p", "pico", "Pico", "PICO"],
  },
  unitsShort: ["R", "r", "Ω", "F", "f", "H", "h"],
  unitsLong: [
    "OHM", "Ohm", "ohm", "ohms",
    "FARAD", "Farad", "farad",
    "HENRY", "Henry", "henry"
  ],
  getMultiplier: function(s) {
    if (this.prefixes.giga.includes(s)) return 1e9;
    if (this.prefixes.mega.includes(s)) return 1e6;
    if (this.prefixes.kilo.includes(s)) return 1e3;
    if (this.prefixes.milli.includes(s)) return 1e-3;
    if (this.prefixes.micro.includes(s)) return 1e-6;
    if (this.prefixes.nano.includes(s)) return 1e-9;
    if (this.prefixes.pico.includes(s)) return 1e-12;
    return 1;
  },
  valueRegex: null,
}

function initUtils() {
  var allPrefixes = units.prefixes.giga
    .concat(units.prefixes.mega)
    .concat(units.prefixes.kilo)
    .concat(units.prefixes.milli)
    .concat(units.prefixes.micro)
    .concat(units.prefixes.nano)
    .concat(units.prefixes.pico);
  var allUnits = units.unitsShort.concat(units.unitsLong);
  units.valueRegex = new RegExp("^([0-9\.]+)" +
    "\\s*(" + allPrefixes.join("|") + ")?" +
    "(" + allUnits.join("|") + ")?" +
    "(\\b.*)?$", "");
  units.valueAltRegex = new RegExp("^([0-9]*)" +
    "(" + units.unitsShort.join("|") + ")?" +
    "([GgMmKkUuNnPp])?" +
    "([0-9]*)" +
    "(\\b.*)?$", "");
  if (config.fields.includes("Value")) {
    var index = config.fields.indexOf("Value");
    pcbdata.bom["parsedValues"] = {};
    for (var id in pcbdata.bom.fields) {
      pcbdata.bom.parsedValues[id] = parseValue(pcbdata.bom.fields[id][index])
    }
  }
}

function parseValue(val, ref) {
  var inferUnit = (unit, ref) => {
    if (unit) {
      unit = unit.toLowerCase();
      if (unit == 'Ω' || unit == "ohm" || unit == "ohms") {
        unit = 'r';
      }
      unit = unit[0];
    } else {
      ref = /^([a-z]+)\d+$/i.exec(ref);
      if (ref) {
        ref = ref[1].toLowerCase();
        if (ref == "c") unit = 'f';
        else if (ref == "l") unit = 'h';
        else if (ref == "r" || ref == "rv") unit = 'r';
        else unit = null;
      }
    }
    return unit;
  };
  val = val.replace(/,/g, "");
  var match = units.valueRegex.exec(val);
  var unit;
  if (match) {
    val = parseFloat(match[1]);
    if (match[2]) {
      val = val * units.getMultiplier(match[2]);
    }
    unit = inferUnit(match[3], ref);
    if (!unit) return null;
    else return {
      val: val,
      unit: unit,
      extra: match[4],
    }
  }
  match = units.valueAltRegex.exec(val);
  if (match && (match[1] || match[4])) {
    val = parseFloat(match[1] + "." + match[4]);
    if (match[3]) {
      val = val * units.getMultiplier(match[3]);
    }
    unit = inferUnit(match[2], ref);
    if (!unit) return null;
    else return {
      val: val,
      unit: unit,
      extra: match[5],
    }
  }
  return null;
}

function valueCompare(a, b, stra, strb) {
  if (a === null && b === null) {
    // Failed to parse both values, compare them as strings.
    if (stra != strb) return stra > strb ? 1 : -1;
    else return 0;
  } else if (a === null) {
    return 1;
  } else if (b === null) {
    return -1;
  } else {
    if (a.unit != b.unit) return a.unit > b.unit ? 1 : -1;
    else if (a.val != b.val) return a.val > b.val ? 1 : -1;
    else if (a.extra != b.extra) return a.extra > b.extra ? 1 : -1;
    else return 0;
  }
}

function validateSaveImgDimension(element) {
  var valid = false;
  var intValue = 0;
  if (/^[1-9]\d*$/.test(element.value)) {
    intValue = parseInt(element.value);
    if (intValue <= 16000) {
      valid = true;
    }
  }
  if (valid) {
    element.classList.remove("invalid");
  } else {
    element.classList.add("invalid");
  }
  return intValue;
}

function saveImage(layer) {
  var width = validateSaveImgDimension(document.getElementById("render-save-width"));
  var height = validateSaveImgDimension(document.getElementById("render-save-height"));
  var bgcolor = null;
  if (!document.getElementById("render-save-transparent").checked) {
    var style = getComputedStyle(topmostdiv);
    bgcolor = style.getPropertyValue("background-color");
  }
  if (!width || !height) return;

  // Prepare image
  var canvas = document.createElement("canvas");
  var layerdict = {
    transform: {
      x: 0,
      y: 0,
      s: 1,
      panx: 0,
      pany: 0,
      zoom: 1,
    },
    bg: canvas,
    fab: canvas,
    silk: canvas,
    highlight: canvas,
    layer: layer,
  }
  // Do the rendering
  recalcLayerScale(layerdict, width, height);
  prepareLayer(layerdict);
  clearCanvas(canvas, bgcolor);
  drawBackground(layerdict, false);
  drawHighlightsOnLayer(layerdict, false);

  // Save image
  var imgdata = canvas.toDataURL("image/png");

  var filename = pcbdata.metadata.title;
  if (pcbdata.metadata.revision) {
    filename += `.${pcbdata.metadata.revision}`;
  }
  filename += `.${layer}.png`;
  saveFile(filename, dataURLtoBlob(imgdata));
}

function saveSettings() {
  var data = {
    type: "InteractiveHtmlBom settings",
    version: 1,
    pcbmetadata: pcbdata.metadata,
    settings: settings,
  }
  var blob = new Blob([JSON.stringify(data, null, 4)], {
    type: "application/json"
  });
  saveFile(`${pcbdata.metadata.title}.settings.json`, blob);
}

function loadSettings() {
  var input = document.createElement("input");
  input.type = "file";
  input.accept = ".settings.json";
  input.onchange = function(e) {
    var file = e.target.files[0];
    var reader = new FileReader();
    reader.onload = readerEvent => {
      var content = readerEvent.target.result;
      var newSettings;
      try {
        newSettings = JSON.parse(content);
      } catch (e) {
        alert("Selected file is not InteractiveHtmlBom settings file.");
        return;
      }
      if (newSettings.type != "InteractiveHtmlBom settings") {
        alert("Selected file is not InteractiveHtmlBom settings file.");
        return;
      }
      var metadataMatches = newSettings.hasOwnProperty("pcbmetadata");
      if (metadataMatches) {
        for (var k in pcbdata.metadata) {
          if (!newSettings.pcbmetadata.hasOwnProperty(k) || newSettings.pcbmetadata[k] != pcbdata.metadata[k]) {
            metadataMatches = false;
          }
        }
      }
      if (!metadataMatches) {
        var currentMetadata = JSON.stringify(pcbdata.metadata, null, 4);
        var fileMetadata = JSON.stringify(newSettings.pcbmetadata, null, 4);
        if (!confirm(
            `Settins file metadata does not match current metadata.\n\n` +
            `Page metadata:\n${currentMetadata}\n\n` +
            `Settings file metadata:\n${fileMetadata}\n\n` +
            `Press OK if you would like to import settings anyway.`)) {
          return;
        }
      }
      overwriteSettings(newSettings.settings);
    }
    reader.readAsText(file, 'UTF-8');
  }
  input.click();
}

function overwriteSettings(newSettings) {
  initDone = false;
  Object.assign(settings, newSettings);
  writeStorage("bomlayout", settings.bomlayout);
  writeStorage("bommode", settings.bommode);
  writeStorage("canvaslayout", settings.canvaslayout);
  writeStorage("bomCheckboxes", settings.checkboxes.join(","));
  document.getElementById("bomCheckboxes").value = settings.checkboxes.join(",");
  for (var checkbox of settings.checkboxes) {
    writeStorage("checkbox_" + checkbox, settings.checkboxStoredRefs[checkbox]);
  }
  writeStorage("markWhenChecked", settings.markWhenChecked);
  padsVisible(settings.renderPads);
  document.getElementById("padsCheckbox").checked = settings.renderPads;
  fabricationVisible(settings.renderFabrication);
  document.getElementById("fabricationCheckbox").checked = settings.renderFabrication;
  silkscreenVisible(settings.renderSilkscreen);
  document.getElementById("silkscreenCheckbox").checked = settings.renderSilkscreen;
  referencesVisible(settings.renderReferences);
  document.getElementById("referencesCheckbox").checked = settings.renderReferences;
  valuesVisible(settings.renderValues);
  document.getElementById("valuesCheckbox").checked = settings.renderValues;
  tracksVisible(settings.renderTracks);
  document.getElementById("tracksCheckbox").checked = settings.renderTracks;
  zonesVisible(settings.renderZones);
  document.getElementById("zonesCheckbox").checked = settings.renderZones;
  dnpOutline(settings.renderDnpOutline);
  document.getElementById("dnpOutlineCheckbox").checked = settings.renderDnpOutline;
  setRedrawOnDrag(settings.redrawOnDrag);
  document.getElementById("dragCheckbox").checked = settings.redrawOnDrag;
  setDarkMode(settings.darkMode);
  document.getElementById("darkmodeCheckbox").checked = settings.darkMode;
  setHighlightPin1(settings.highlightpin1);
  document.getElementById("highlightpin1Checkbox").checked = settings.highlightpin1;
  showFootprints(settings.show_footprints);
  writeStorage("boardRotation", settings.boardRotation);
  document.getElementById("boardRotation").value = settings.boardRotation / 5;
  document.getElementById("rotationDegree").textContent = settings.boardRotation;
  initDone = true;
  prepCheckboxes();
  changeBomLayout(settings.bomlayout);
}

function saveFile(filename, blob) {
  var link = document.createElement("a");
  var objurl = URL.createObjectURL(blob);
  link.download = filename;
  link.href = objurl;
  link.click();
}

function dataURLtoBlob(dataurl) {
  var arr = dataurl.split(','),
    mime = arr[0].match(/:(.*?);/)[1],
    bstr = atob(arr[1]),
    n = bstr.length,
    u8arr = new Uint8Array(n);
  while (n--) {
    u8arr[n] = bstr.charCodeAt(n);
  }
  return new Blob([u8arr], {
    type: mime
  });
}

var settings = {
  canvaslayout: "default",
  bomlayout: "default",
  bommode: "grouped",
  checkboxes: [],
  checkboxStoredRefs: {},
  darkMode: false,
  highlightpin1: false,
  redrawOnDrag: true,
  boardRotation: 0,
  renderPads: true,
  renderReferences: true,
  renderValues: true,
  renderSilkscreen: true,
  renderFabrication: true,
  renderDnpOutline: false,
  renderTracks: true,
  renderZones: true,
  columnOrder: [],
  hiddenColumns: [],
}

function initDefaults() {
  settings.bomlayout = readStorage("bomlayout");
  if (settings.bomlayout === null) {
    settings.bomlayout = config.bom_view;
  }
  if (!['bom-only', 'left-right', 'top-bottom'].includes(settings.bomlayout)) {
    settings.bomlayout = config.bom_view;
  }
  settings.bommode = readStorage("bommode");
  if (settings.bommode === null) {
    settings.bommode = "grouped";
  }
  if (!["grouped", "ungrouped", "netlist"].includes(settings.bommode)) {
    settings.bommode = "grouped";
  }
  settings.canvaslayout = readStorage("canvaslayout");
  if (settings.canvaslayout === null) {
    settings.canvaslayout = config.layer_view;
  }
  var bomCheckboxes = readStorage("bomCheckboxes");
  if (bomCheckboxes === null) {
    bomCheckboxes = config.checkboxes;
  }
  settings.checkboxes = bomCheckboxes.split(",").filter((e) => e);
  document.getElementById("bomCheckboxes").value = bomCheckboxes;

  settings.markWhenChecked = readStorage("markWhenChecked") || "";
  populateMarkWhenCheckedOptions();

  function initBooleanSetting(storageString, def, elementId, func) {
    var b = readStorage(storageString);
    if (b === null) {
      b = def;
    } else {
      b = (b == "true");
    }
    document.getElementById(elementId).checked = b;
    func(b);
  }

  initBooleanSetting("padsVisible", config.show_pads, "padsCheckbox", padsVisible);
  initBooleanSetting("fabricationVisible", config.show_fabrication, "fabricationCheckbox", fabricationVisible);
  initBooleanSetting("silkscreenVisible", config.show_silkscreen, "silkscreenCheckbox", silkscreenVisible);
  initBooleanSetting("referencesVisible", true, "referencesCheckbox", referencesVisible);
  initBooleanSetting("valuesVisible", true, "valuesCheckbox", valuesVisible);
  if ("tracks" in pcbdata) {
    initBooleanSetting("tracksVisible", true, "tracksCheckbox", tracksVisible);
    initBooleanSetting("zonesVisible", true, "zonesCheckbox", zonesVisible);
  } else {
    document.getElementById("tracksAndZonesCheckboxes").style.display = "none";
    tracksVisible(false);
    zonesVisible(false);
  }
  initBooleanSetting("dnpOutline", false, "dnpOutlineCheckbox", dnpOutline);
  initBooleanSetting("redrawOnDrag", config.redraw_on_drag, "dragCheckbox", setRedrawOnDrag);
  initBooleanSetting("darkmode", config.dark_mode, "darkmodeCheckbox", setDarkMode);
  initBooleanSetting("highlightpin1", config.highlight_pin1, "highlightpin1Checkbox", setHighlightPin1);

  var fields = ["checkboxes", "References"].concat(config.fields).concat(["Quantity"]);
  var hcols = JSON.parse(readStorage("hiddenColumns"));
  if (hcols === null) {
    hcols = [];
  }
  settings.hiddenColumns = hcols.filter(e => fields.includes(e));

  var cord = JSON.parse(readStorage("columnOrder"));
  if (cord === null) {
    cord = fields;
  } else {
    cord = cord.filter(e => fields.includes(e));
    if (cord.length != fields.length)
      cord = fields;
  }
  settings.columnOrder = cord;

  settings.boardRotation = readStorage("boardRotation");
  if (settings.boardRotation === null) {
    settings.boardRotation = config.board_rotation * 5;
  } else {
    settings.boardRotation = parseInt(settings.boardRotation);
  }
  document.getElementById("boardRotation").value = settings.boardRotation / 5;
  document.getElementById("rotationDegree").textContent = settings.boardRotation;
}

// Helper classes for user js callbacks.

const IBOM_EVENT_TYPES = {
  ALL: "all",
  HIGHLIGHT_EVENT: "highlightEvent",
  CHECKBOX_CHANGE_EVENT: "checkboxChangeEvent",
  BOM_BODY_CHANGE_EVENT: "bomBodyChangeEvent",
}

const EventHandler = {
  callbacks: {},
  init: function() {
    for (eventType of Object.values(IBOM_EVENT_TYPES))
      this.callbacks[eventType] = [];
  },
  registerCallback: function(eventType, callback) {
    this.callbacks[eventType].push(callback);
  },
  emitEvent: function(eventType, eventArgs) {
    event = {
      eventType: eventType,
      args: eventArgs,
    }
    var callback;
    for (callback of this.callbacks[eventType])
      callback(event);
    for (callback of this.callbacks[IBOM_EVENT_TYPES.ALL])
      callback(event);
  }
}
EventHandler.init();

///////////////////////////////////////////////

///////////////////////////////////////////////
/* PCB rendering code */

var emptyContext2d = document.createElement("canvas").getContext("2d");

function deg2rad(deg) {
  return deg * Math.PI / 180;
}

function calcFontPoint(linepoint, text, offsetx, offsety, tilt) {
  var point = [
    linepoint[0] * text.width + offsetx,
    linepoint[1] * text.height + offsety
  ];
  // This approximates pcbnew behavior with how text tilts depending on horizontal justification
  point[0] -= (linepoint[1] + 0.5 * (1 + text.justify[0])) * text.height * tilt;
  return point;
}

function drawText(ctx, text, color) {
  if ("ref" in text && !settings.renderReferences) return;
  if ("val" in text && !settings.renderValues) return;
  ctx.save();
  ctx.fillStyle = color;
  ctx.strokeStyle = color;
  ctx.lineCap = "round";
  ctx.lineJoin = "round";
  ctx.lineWidth = text.thickness;
  if ("svgpath" in text) {
    ctx.stroke(new Path2D(text.svgpath));
    ctx.restore();
    return;
  }
  if ("polygons" in text) {
    ctx.fill(getPolygonsPath(text));
    ctx.restore();
    return;
  }
  ctx.translate(...text.pos);
  ctx.translate(text.thickness * 0.5, 0);
  var angle = -text.angle;
  if (text.attr.includes("mirrored")) {
    ctx.scale(-1, 1);
    angle = -angle;
  }
  var tilt = 0;
  if (text.attr.includes("italic")) {
    tilt = 0.125;
  }
  var interline = text.height * 1.5 + text.thickness;
  var txt = text.text.split("\n");
  // KiCad ignores last empty line.
  if (txt[txt.length - 1] == '') txt.pop();
  ctx.rotate(deg2rad(angle));
  var offsety = (1 - text.justify[1]) / 2 * text.height; // One line offset
  offsety -= (txt.length - 1) * (text.justify[1] + 1) / 2 * interline; // Multiline offset
  for (var i in txt) {
    var lineWidth = text.thickness + interline / 2 * tilt;
    for (var j = 0; j < txt[i].length; j++) {
      if (txt[i][j] == '\t') {
        var fourSpaces = 4 * pcbdata.font_data[' '].w * text.width;
        lineWidth += fourSpaces - lineWidth % fourSpaces;
      } else {
        if (txt[i][j] == '~') {
          j++;
          if (j == txt[i].length)
            break;
        }
        lineWidth += pcbdata.font_data[txt[i][j]].w * text.width;
      }
    }
    var offsetx = -lineWidth * (text.justify[0] + 1) / 2;
    var inOverbar = false;
    for (var j = 0; j < txt[i].length; j++) {
      if (txt[i][j] == '\t') {
        var fourSpaces = 4 * pcbdata.font_data[' '].w * text.width;
        offsetx += fourSpaces - offsetx % fourSpaces;
        continue;
      } else if (txt[i][j] == '~') {
        j++;
        if (j == txt[i].length)
          break;
        if (txt[i][j] != '~') {
          inOverbar = !inOverbar;
        }
      }
      var glyph = pcbdata.font_data[txt[i][j]];
      if (inOverbar) {
        var overbarStart = [offsetx, -text.height * 1.4 + offsety];
        var overbarEnd = [offsetx + text.width * glyph.w, overbarStart[1]];

        if (!lastHadOverbar) {
          overbarStart[0] += text.height * 1.4 * tilt;
          lastHadOverbar = true;
        }
        ctx.beginPath();
        ctx.moveTo(...overbarStart);
        ctx.lineTo(...overbarEnd);
        ctx.stroke();
      } else {
        lastHadOverbar = false;
      }
      for (var line of glyph.l) {
        ctx.beginPath();
        ctx.moveTo(...calcFontPoint(line[0], text, offsetx, offsety, tilt));
        for (var k = 1; k < line.length; k++) {
          ctx.lineTo(...calcFontPoint(line[k], text, offsetx, offsety, tilt));
        }
        ctx.stroke();
      }
      offsetx += glyph.w * text.width;
    }
    offsety += interline;
  }
  ctx.restore();
}

function drawedge(ctx, scalefactor, edge, color) {
  ctx.strokeStyle = color;
  ctx.fillStyle = color;
  ctx.lineWidth = Math.max(1 / scalefactor, edge.width);
  ctx.lineCap = "round";
  ctx.lineJoin = "round";
  if ("svgpath" in edge) {
    ctx.stroke(new Path2D(edge.svgpath));
  } else {
    ctx.beginPath();
    if (edge.type == "segment") {
      ctx.moveTo(...edge.start);
      ctx.lineTo(...edge.end);
    }
    if (edge.type == "rect") {
      ctx.moveTo(...edge.start);
      ctx.lineTo(edge.start[0], edge.end[1]);
      ctx.lineTo(...edge.end);
      ctx.lineTo(edge.end[0], edge.start[1]);
      ctx.lineTo(...edge.start);
    }
    if (edge.type == "arc") {
      ctx.arc(
        ...edge.start,
        edge.radius,
        deg2rad(edge.startangle),
        deg2rad(edge.endangle));
    }
    if (edge.type == "circle") {
      ctx.arc(
        ...edge.start,
        edge.radius,
        0, 2 * Math.PI);
      ctx.closePath();
    }
    if (edge.type == "curve") {
      ctx.moveTo(...edge.start);
      ctx.bezierCurveTo(...edge.cpa, ...edge.cpb, ...edge.end);
    }
    if("filled" in edge && edge.filled)
      ctx.fill();
    else
      ctx.stroke();
  }
}

function getChamferedRectPath(size, radius, chamfpos, chamfratio) {
  // chamfpos is a bitmask, left = 1, right = 2, bottom left = 4, bottom right = 8
  var path = new Path2D();
  var width = size[0];
  var height = size[1];
  var x = width * -0.5;
  var y = height * -0.5;
  var chamfOffset = Math.min(width, height) * chamfratio;
  path.moveTo(x, 0);
  if (chamfpos & 4) {
    path.lineTo(x, y + height - chamfOffset);
    path.lineTo(x + chamfOffset, y + height);
    path.lineTo(0, y + height);
  } else {
    path.arcTo(x, y + height, x + width, y + height, radius);
  }
  if (chamfpos & 8) {
    path.lineTo(x + width - chamfOffset, y + height);
    path.lineTo(x + width, y + height - chamfOffset);
    path.lineTo(x + width, 0);
  } else {
    path.arcTo(x + width, y + height, x + width, y, radius);
  }
  if (chamfpos & 2) {
    path.lineTo(x + width, y + chamfOffset);
    path.lineTo(x + width - chamfOffset, y);
    path.lineTo(0, y);
  } else {
    path.arcTo(x + width, y, x, y, radius);
  }
  if (chamfpos & 1) {
    path.lineTo(x + chamfOffset, y);
    path.lineTo(x, y + chamfOffset);
    path.lineTo(x, 0);
  } else {
    path.arcTo(x, y, x, y + height, radius);
  }
  path.closePath();
  return path;
}

function getOblongPath(size) {
  return getChamferedRectPath(size, Math.min(size[0], size[1]) / 2, 0, 0);
}

function getPolygonsPath(shape) {
  if (shape.path2d) {
    return shape.path2d;
  }
  if ("svgpath" in shape) {
    shape.path2d = new Path2D(shape.svgpath);
  } else {
    var path = new Path2D();
    for (var polygon of shape.polygons) {
      path.moveTo(...polygon[0]);
      for (var i = 1; i < polygon.length; i++) {
        path.lineTo(...polygon[i]);
      }
      path.closePath();
    }
    shape.path2d = path;
  }
  return shape.path2d;
}

function drawPolygonShape(ctx, scalefactor, shape, color) {
  ctx.save();
  if (!("svgpath" in shape)) {
    ctx.translate(...shape.pos);
    ctx.rotate(deg2rad(-shape.angle));
  }
  if("filled" in shape && !shape.filled) {
    ctx.strokeStyle = color;
    ctx.lineWidth = Math.max(1 / scalefactor, shape.width);
    ctx.lineCap = "round";
    ctx.lineJoin = "round";
    ctx.stroke(getPolygonsPath(shape));
  } else {
    ctx.fillStyle = color;
    ctx.fill(getPolygonsPath(shape));
  }
  ctx.restore();
}

function drawDrawing(ctx, scalefactor, drawing, color) {
  if (["segment", "arc", "circle", "curve", "rect"].includes(drawing.type)) {
    drawedge(ctx, scalefactor, drawing, color);
  } else if (drawing.type == "polygon") {
    drawPolygonShape(ctx, scalefactor, drawing, color);
  } else {
    drawText(ctx, drawing, color);
  }
}

function getCirclePath(radius) {
  var path = new Path2D();
  path.arc(0, 0, radius, 0, 2 * Math.PI);
  path.closePath();
  return path;
}

function getCachedPadPath(pad) {
  if (!pad.path2d) {
    // if path2d is not set, build one and cache it on pad object
    if (pad.shape == "rect") {
      pad.path2d = new Path2D();
      pad.path2d.rect(...pad.size.map(c => -c * 0.5), ...pad.size);
    } else if (pad.shape == "oval") {
      pad.path2d = getOblongPath(pad.size);
    } else if (pad.shape == "circle") {
      pad.path2d = getCirclePath(pad.size[0] / 2);
    } else if (pad.shape == "roundrect") {
      pad.path2d = getChamferedRectPath(pad.size, pad.radius, 0, 0);
    } else if (pad.shape == "chamfrect") {
      pad.path2d = getChamferedRectPath(pad.size, pad.radius, pad.chamfpos, pad.chamfratio)
    } else if (pad.shape == "custom") {
      pad.path2d = getPolygonsPath(pad);
    }
  }
  return pad.path2d;
}

function drawPad(ctx, pad, color, outline) {
  ctx.save();
  ctx.translate(...pad.pos);
  ctx.rotate(-deg2rad(pad.angle));
  if (pad.offset) {
    ctx.translate(...pad.offset);
  }
  ctx.fillStyle = color;
  ctx.strokeStyle = color;
  var path = getCachedPadPath(pad);
  if (outline) {
    ctx.stroke(path);
  } else {
    ctx.fill(path);
  }
  ctx.restore();
}

function drawPadHole(ctx, pad, padHoleColor) {
  if (pad.type != "th") return;
  ctx.save();
  ctx.translate(...pad.pos);
  ctx.rotate(-deg2rad(pad.angle));
  ctx.fillStyle = padHoleColor;
  if (pad.drillshape == "oblong") {
    ctx.fill(getOblongPath(pad.drillsize));
  } else {
    ctx.fill(getCirclePath(pad.drillsize[0] / 2));
  }
  ctx.restore();
}

function drawFootprint(ctx, layer, scalefactor, footprint, colors, highlight, outline) {
  if (highlight) {
    // draw bounding box
    if (footprint.layer == layer) {
      ctx.save();
      ctx.globalAlpha = 0.2;
      ctx.translate(...footprint.bbox.pos);
      ctx.rotate(deg2rad(-footprint.bbox.angle));
      ctx.translate(...footprint.bbox.relpos);
      ctx.fillStyle = colors.pad;
      ctx.fillRect(0, 0, ...footprint.bbox.size);
      ctx.globalAlpha = 1;
      ctx.strokeStyle = colors.pad;
      ctx.strokeRect(0, 0, ...footprint.bbox.size);
      ctx.restore();
    }
  }
  // draw drawings
  for (var drawing of footprint.drawings) {
    if (drawing.layer == layer) {
      drawDrawing(ctx, scalefactor, drawing.drawing, colors.pad);
    }
  }
  // draw pads
  if (settings.renderPads) {
    for (var pad of footprint.pads) {
      if (pad.layers.includes(layer)) {
        drawPad(ctx, pad, colors.pad, outline);
        if (pad.pin1 && settings.highlightpin1) {
          drawPad(ctx, pad, colors.outline, true);
        }
      }
    }
    for (var pad of footprint.pads) {
      drawPadHole(ctx, pad, colors.padHole);
    }
  }
}

function drawEdgeCuts(canvas, scalefactor) {
  var ctx = canvas.getContext("2d");
  var edgecolor = getComputedStyle(topmostdiv).getPropertyValue('--pcb-edge-color');
  for (var edge of pcbdata.edges) {
    drawDrawing(ctx, scalefactor, edge, edgecolor);
  }
}

function drawFootprints(canvas, layer, scalefactor, highlight) {
  var ctx = canvas.getContext("2d");
  ctx.lineWidth = 3 / scalefactor;
  var style = getComputedStyle(topmostdiv);

  var colors = {
    pad: style.getPropertyValue('--pad-color'),
    padHole: style.getPropertyValue('--pad-hole-color'),
    outline: style.getPropertyValue('--pin1-outline-color'),
  }

  for (var i = 0; i < pcbdata.footprints.length; i++) {
    var mod = pcbdata.footprints[i];
    var outline = settings.renderDnpOutline && pcbdata.bom.skipped.includes(i);
    var h = highlightedFootprints.includes(i);
    var d = markedFootprints.has(i);
    if (highlight) {
      if(h && d) {
        colors.pad = style.getPropertyValue('--pad-color-highlight-both');
        colors.outline = style.getPropertyValue('--pin1-outline-color-highlight-both');
      } else if (h) {
        colors.pad = style.getPropertyValue('--pad-color-highlight');
        colors.outline = style.getPropertyValue('--pin1-outline-color-highlight');
      } else if (d) {
        colors.pad = style.getPropertyValue('--pad-color-highlight-marked');
        colors.outline = style.getPropertyValue('--pin1-outline-color-highlight-marked');
      }
    }
    if( h || d || !highlight) {
      drawFootprint(ctx, layer, scalefactor, mod, colors, highlight, outline);
    }
  }
}

function drawBgLayer(layername, canvas, layer, scalefactor, edgeColor, polygonColor, textColor) {
  var ctx = canvas.getContext("2d");
  for (var d of pcbdata.drawings[layername][layer]) {
    if (["segment", "arc", "circle", "curve", "rect"].includes(d.type)) {
      drawedge(ctx, scalefactor, d, edgeColor);
    } else if (d.type == "polygon") {
      drawPolygonShape(ctx, scalefactor, d, polygonColor);
    } else {
      drawText(ctx, d, textColor);
    }
  }
}

function drawTracks(canvas, layer, color, highlight) {
  ctx = canvas.getContext("2d");
  ctx.strokeStyle = color;
  ctx.lineCap = "round";
  for (var track of pcbdata.tracks[layer]) {
    if (highlight && highlightedNet != track.net) continue;
    ctx.lineWidth = track.width;
    ctx.beginPath();
    if ('radius' in track) {
      ctx.arc(
        ...track.center,
        track.radius,
        deg2rad(track.startangle),
        deg2rad(track.endangle));
    } else {
      ctx.moveTo(...track.start);
      ctx.lineTo(...track.end);
    }
    ctx.stroke();
  }
}

function drawZones(canvas, layer, color, highlight) {
  ctx = canvas.getContext("2d");
  ctx.strokeStyle = color;
  ctx.fillStyle = color;
  ctx.lineJoin = "round";
  for (var zone of pcbdata.zones[layer]) {
    if (!zone.path2d) {
      zone.path2d = getPolygonsPath(zone);
    }
    if (highlight && highlightedNet != zone.net) continue;
    ctx.fill(zone.path2d);
    if (zone.width > 0) {
      ctx.lineWidth = zone.width;
      ctx.stroke(zone.path2d);
    }
  }
}

function clearCanvas(canvas, color = null) {
  var ctx = canvas.getContext("2d");
  ctx.save();
  ctx.setTransform(1, 0, 0, 1, 0, 0);
  if (color) {
    ctx.fillStyle = color;
    ctx.fillRect(0, 0, canvas.width, canvas.height);
  } else {
    if (!window.matchMedia("print").matches)
      ctx.clearRect(0, 0, canvas.width, canvas.height);
  }
  ctx.restore();
}

function drawNets(canvas, layer, highlight) {
  var style = getComputedStyle(topmostdiv);
  if (settings.renderTracks) {
    var trackColor = style.getPropertyValue(highlight ? '--track-color-highlight' : '--track-color');
    drawTracks(canvas, layer, trackColor, highlight);
  }
  if (settings.renderZones) {
    var zoneColor = style.getPropertyValue(highlight ? '--zone-color-highlight' : '--zone-color');
    drawZones(canvas, layer, zoneColor, highlight);
  }
  if (highlight && settings.renderPads) {
    var padColor = style.getPropertyValue('--pad-color-highlight');
    var padHoleColor = style.getPropertyValue('--pad-hole-color');
    var ctx = canvas.getContext("2d");
    for (var footprint of pcbdata.footprints) {
      // draw pads
      var padDrawn = false;
      for (var pad of footprint.pads) {
        if (highlightedNet != pad.net) continue;
        if (pad.layers.includes(layer)) {
          drawPad(ctx, pad, padColor, false);
          padDrawn = true;
        }
      }
      if (padDrawn) {
        // redraw all pad holes because some pads may overlap
        for (var pad of footprint.pads) {
          drawPadHole(ctx, pad, padHoleColor);
        }
      }
    }
  }
}

function drawHighlightsOnLayer(canvasdict, clear = true) {
  if (clear) {
    clearCanvas(canvasdict.highlight);
  }
  if (markedFootprints.size > 0 || highlightedFootprints.length > 0) {
    drawFootprints(canvasdict.highlight, canvasdict.layer,
      canvasdict.transform.s * canvasdict.transform.zoom, true);
  }
  if (highlightedNet !== null) {
    drawNets(canvasdict.highlight, canvasdict.layer, true);
  }
}

function drawHighlights() {
  drawHighlightsOnLayer(allcanvas.front);
  drawHighlightsOnLayer(allcanvas.back);
}

function drawBackground(canvasdict, clear = true) {
  if (clear) {
    clearCanvas(canvasdict.bg);
    clearCanvas(canvasdict.fab);
    clearCanvas(canvasdict.silk);
  }

  drawNets(canvasdict.bg, canvasdict.layer, false);
  drawFootprints(canvasdict.bg, canvasdict.layer,
    canvasdict.transform.s * canvasdict.transform.zoom, false);

  drawEdgeCuts(canvasdict.bg, canvasdict.transform.s * canvasdict.transform.zoom);

  var style = getComputedStyle(topmostdiv);
  var edgeColor = style.getPropertyValue('--silkscreen-edge-color');
  var polygonColor = style.getPropertyValue('--silkscreen-polygon-color');
  var textColor = style.getPropertyValue('--silkscreen-text-color');
  if (settings.renderSilkscreen) {
    drawBgLayer(
      "silkscreen", canvasdict.silk, canvasdict.layer,
      canvasdict.transform.s * canvasdict.transform.zoom,
      edgeColor, polygonColor, textColor);
  }
  edgeColor = style.getPropertyValue('--fabrication-edge-color');
  polygonColor = style.getPropertyValue('--fabrication-polygon-color');
  textColor = style.getPropertyValue('--fabrication-text-color');
  if (settings.renderFabrication) {
    drawBgLayer(
      "fabrication", canvasdict.fab, canvasdict.layer,
      canvasdict.transform.s * canvasdict.transform.zoom,
      edgeColor, polygonColor, textColor);
  }
}

function prepareCanvas(canvas, flip, transform) {
  var ctx = canvas.getContext("2d");
  ctx.setTransform(1, 0, 0, 1, 0, 0);
  ctx.scale(transform.zoom, transform.zoom);
  ctx.translate(transform.panx, transform.pany);
  if (flip) {
    ctx.scale(-1, 1);
  }
  ctx.translate(transform.x, transform.y);
  ctx.rotate(deg2rad(settings.boardRotation));
  ctx.scale(transform.s, transform.s);
}

function prepareLayer(canvasdict) {
  var flip = (canvasdict.layer == "B");
  for (var c of ["bg", "fab", "silk", "highlight"]) {
    prepareCanvas(canvasdict[c], flip, canvasdict.transform);
  }
}

function rotateVector(v, angle) {
  angle = deg2rad(angle);
  return [
    v[0] * Math.cos(angle) - v[1] * Math.sin(angle),
    v[0] * Math.sin(angle) + v[1] * Math.cos(angle)
  ];
}

function applyRotation(bbox) {
  var corners = [
    [bbox.minx, bbox.miny],
    [bbox.minx, bbox.maxy],
    [bbox.maxx, bbox.miny],
    [bbox.maxx, bbox.maxy],
  ];
  corners = corners.map((v) => rotateVector(v, settings.boardRotation));
  return {
    minx: corners.reduce((a, v) => Math.min(a, v[0]), Infinity),
    miny: corners.reduce((a, v) => Math.min(a, v[1]), Infinity),
    maxx: corners.reduce((a, v) => Math.max(a, v[0]), -Infinity),
    maxy: corners.reduce((a, v) => Math.max(a, v[1]), -Infinity),
  }
}

function recalcLayerScale(layerdict, width, height) {
  var bbox = applyRotation(pcbdata.edges_bbox);
  var scalefactor = 0.98 * Math.min(
    width / (bbox.maxx - bbox.minx),
    height / (bbox.maxy - bbox.miny)
  );
  if (scalefactor < 0.1) {
    scalefactor = 1;
  }
  layerdict.transform.s = scalefactor;
  var flip = (layerdict.layer == "B");
  if (flip) {
    layerdict.transform.x = -((bbox.maxx + bbox.minx) * scalefactor + width) * 0.5;
  } else {
    layerdict.transform.x = -((bbox.maxx + bbox.minx) * scalefactor - width) * 0.5;
  }
  layerdict.transform.y = -((bbox.maxy + bbox.miny) * scalefactor - height) * 0.5;
  for (var c of ["bg", "fab", "silk", "highlight"]) {
    canvas = layerdict[c];
    canvas.width = width;
    canvas.height = height;
    canvas.style.width = (width / devicePixelRatio) + "px";
    canvas.style.height = (height / devicePixelRatio) + "px";
  }
}

function redrawCanvas(layerdict) {
  prepareLayer(layerdict);
  drawBackground(layerdict);
  drawHighlightsOnLayer(layerdict);
}

function resizeCanvas(layerdict) {
  var canvasdivid = {
    "F": "frontcanvas",
    "B": "backcanvas"
  } [layerdict.layer];
  var width = document.getElementById(canvasdivid).clientWidth * devicePixelRatio;
  var height = document.getElementById(canvasdivid).clientHeight * devicePixelRatio;
  recalcLayerScale(layerdict, width, height);
  redrawCanvas(layerdict);
}

function resizeAll() {
  resizeCanvas(allcanvas.front);
  resizeCanvas(allcanvas.back);
}

function pointWithinDistanceToSegment(x, y, x1, y1, x2, y2, d) {
  var A = x - x1;
  var B = y - y1;
  var C = x2 - x1;
  var D = y2 - y1;

  var dot = A * C + B * D;
  var len_sq = C * C + D * D;
  var dx, dy;
  if (len_sq == 0) {
    // start and end of the segment coincide
    dx = x - x1;
    dy = y - y1;
  } else {
    var param = dot / len_sq;
    var xx, yy;
    if (param < 0) {
      xx = x1;
      yy = y1;
    } else if (param > 1) {
      xx = x2;
      yy = y2;
    } else {
      xx = x1 + param * C;
      yy = y1 + param * D;
    }
    dx = x - xx;
    dy = y - yy;
  }
  return dx * dx + dy * dy <= d * d;
}

function modulo(n, mod) {
  return ((n % mod) + mod) % mod;
}

function pointWithinDistanceToArc(x, y, xc, yc, radius, startangle, endangle, d) {
  var dx = x - xc;
  var dy = y - yc;
  var r_sq = dx * dx + dy * dy;
  var rmin = Math.max(0, radius - d);
  var rmax = radius + d;

  if (r_sq < rmin * rmin || r_sq > rmax * rmax)
    return false;

  var angle1 = modulo(deg2rad(startangle), 2 * Math.PI);
  var dx1 = xc + radius * Math.cos(angle1) - x;
  var dy1 = yc + radius * Math.sin(angle1) - y;
  if (dx1 * dx1 + dy1 * dy1 <= d * d)
    return true;

  var angle2 = modulo(deg2rad(endangle), 2 * Math.PI);
  var dx2 = xc + radius * Math.cos(angle2) - x;
  var dy2 = yc + radius * Math.sin(angle2) - y;
  if (dx2 * dx2 + dy2 * dy2 <= d * d)
    return true;

  var angle = modulo(Math.atan2(dy, dx), 2 * Math.PI);
  if (angle1 > angle2)
    return (angle >= angle2 || angle <= angle1);
  else
    return (angle >= angle1 && angle <= angle2);
}

function pointWithinPad(x, y, pad) {
  var v = [x - pad.pos[0], y - pad.pos[1]];
  v = rotateVector(v, pad.angle);
  if (pad.offset) {
    v[0] -= pad.offset[0];
    v[1] -= pad.offset[1];
  }
  return emptyContext2d.isPointInPath(getCachedPadPath(pad), ...v);
}

function netHitScan(layer, x, y) {
  // Check track segments
  if (settings.renderTracks && pcbdata.tracks) {
    for (var track of pcbdata.tracks[layer]) {
      if ('radius' in track) {
        if (pointWithinDistanceToArc(x, y, ...track.center, track.radius, track.startangle, track.endangle, track.width / 2)) {
          return track.net;
        }
      } else {
        if (pointWithinDistanceToSegment(x, y, ...track.start, ...track.end, track.width / 2)) {
          return track.net;
        }
      }
    }
  }
  // Check pads
  if (settings.renderPads) {
    for (var footprint of pcbdata.footprints) {
      for (var pad of footprint.pads) {
        if (pad.layers.includes(layer) && pointWithinPad(x, y, pad)) {
          return pad.net;
        }
      }
    }
  }
  return null;
}

function pointWithinFootprintBbox(x, y, bbox) {
  var v = [x - bbox.pos[0], y - bbox.pos[1]];
  v = rotateVector(v, bbox.angle);
  return bbox.relpos[0] <= v[0] && v[0] <= bbox.relpos[0] + bbox.size[0] &&
    bbox.relpos[1] <= v[1] && v[1] <= bbox.relpos[1] + bbox.size[1];
}

function bboxHitScan(layer, x, y) {
  var result = [];
  for (var i = 0; i < pcbdata.footprints.length; i++) {
    var footprint = pcbdata.footprints[i];
    if (footprint.layer == layer) {
      if (pointWithinFootprintBbox(x, y, footprint.bbox)) {
        result.push(i);
      }
    }
  }
  return result;
}

function handlePointerDown(e, layerdict) {
  if (e.button != 0 && e.button != 1) {
    return;
  }
  e.preventDefault();
  e.stopPropagation();

  if (!e.hasOwnProperty("offsetX")) {
    // The polyfill doesn't set this properly
    e.offsetX = e.pageX - e.currentTarget.offsetLeft;
    e.offsetY = e.pageY - e.currentTarget.offsetTop;
  }

  layerdict.pointerStates[e.pointerId] = {
    distanceTravelled: 0,
    lastX: e.offsetX,
    lastY: e.offsetY,
    downTime: Date.now(),
  };
}

function handleMouseClick(e, layerdict) {
  if (!e.hasOwnProperty("offsetX")) {
    // The polyfill doesn't set this properly
    e.offsetX = e.pageX - e.currentTarget.offsetLeft;
    e.offsetY = e.pageY - e.currentTarget.offsetTop;
  }

  var x = e.offsetX;
  var y = e.offsetY;
  var t = layerdict.transform;
  if (layerdict.layer == "B") {
    x = (devicePixelRatio * x / t.zoom - t.panx + t.x) / -t.s;
  } else {
    x = (devicePixelRatio * x / t.zoom - t.panx - t.x) / t.s;
  }
  y = (devicePixelRatio * y / t.zoom - t.y - t.pany) / t.s;
  var v = rotateVector([x, y], -settings.boardRotation);
  if ("nets" in pcbdata) {
    var net = netHitScan(layerdict.layer, ...v);
    if (net !== highlightedNet) {
      netClicked(net);
    }
  }
  if (highlightedNet === null) {
    var footprints = bboxHitScan(layerdict.layer, ...v);
    if (footprints.length > 0) {
      footprintsClicked(footprints);
    }
  }
}

function handlePointerLeave(e, layerdict) {
  e.preventDefault();
  e.stopPropagation();

  if (!settings.redrawOnDrag) {
    redrawCanvas(layerdict);
  }

  delete layerdict.pointerStates[e.pointerId];
}

function resetTransform(layerdict) {
  layerdict.transform.panx = 0;
  layerdict.transform.pany = 0;
  layerdict.transform.zoom = 1;
  redrawCanvas(layerdict);
}

function handlePointerUp(e, layerdict) {
  if (!e.hasOwnProperty("offsetX")) {
    // The polyfill doesn't set this properly
    e.offsetX = e.pageX - e.currentTarget.offsetLeft;
    e.offsetY = e.pageY - e.currentTarget.offsetTop;
  }

  e.preventDefault();
  e.stopPropagation();

  if (e.button == 2) {
    // Reset pan and zoom on right click.
    resetTransform(layerdict);
    layerdict.anotherPointerTapped = false;
    return;
  }

  // We haven't necessarily had a pointermove event since the interaction started, so make sure we update this now
  var ptr = layerdict.pointerStates[e.pointerId];
  ptr.distanceTravelled += Math.abs(e.offsetX - ptr.lastX) + Math.abs(e.offsetY - ptr.lastY);

  if (e.button == 0 && ptr.distanceTravelled < 10 && Date.now() - ptr.downTime <= 500) {
    if (Object.keys(layerdict.pointerStates).length == 1) {
      if (layerdict.anotherPointerTapped) {
        // This is the second pointer coming off of a two-finger tap
        resetTransform(layerdict);
      } else {
        // This is just a regular tap
        handleMouseClick(e, layerdict);
      }
      layerdict.anotherPointerTapped = false;
    } else {
      // This is the first finger coming off of what could become a two-finger tap
      layerdict.anotherPointerTapped = true;
    }
  } else {
    if (!settings.redrawOnDrag) {
      redrawCanvas(layerdict);
    }
    layerdict.anotherPointerTapped = false;
  }

  delete layerdict.pointerStates[e.pointerId];
}

function handlePointerMove(e, layerdict) {
  if (!layerdict.pointerStates.hasOwnProperty(e.pointerId)) {
    return;
  }
  e.preventDefault();
  e.stopPropagation();

  if (!e.hasOwnProperty("offsetX")) {
    // The polyfill doesn't set this properly
    e.offsetX = e.pageX - e.currentTarget.offsetLeft;
    e.offsetY = e.pageY - e.currentTarget.offsetTop;
  }

  var thisPtr = layerdict.pointerStates[e.pointerId];

  var dx = e.offsetX - thisPtr.lastX;
  var dy = e.offsetY - thisPtr.lastY;

  // If this number is low on pointer up, we count the action as a click
  thisPtr.distanceTravelled += Math.abs(dx) + Math.abs(dy);

  if (Object.keys(layerdict.pointerStates).length == 1) {
    // This is a simple drag
    layerdict.transform.panx += devicePixelRatio * dx / layerdict.transform.zoom;
    layerdict.transform.pany += devicePixelRatio * dy / layerdict.transform.zoom;
  } else if (Object.keys(layerdict.pointerStates).length == 2) {
    var otherPtr = Object.values(layerdict.pointerStates).filter((ptr) => ptr != thisPtr)[0];

    var oldDist = Math.sqrt(Math.pow(thisPtr.lastX - otherPtr.lastX, 2) + Math.pow(thisPtr.lastY - otherPtr.lastY, 2));
    var newDist = Math.sqrt(Math.pow(e.offsetX - otherPtr.lastX, 2) + Math.pow(e.offsetY - otherPtr.lastY, 2));

    var scaleFactor = newDist / oldDist;

    if (scaleFactor != NaN) {
      layerdict.transform.zoom *= scaleFactor;

      var zoomd = (1 - scaleFactor) / layerdict.transform.zoom;
      layerdict.transform.panx += devicePixelRatio * otherPtr.lastX * zoomd;
      layerdict.transform.pany += devicePixelRatio * otherPtr.lastY * zoomd;
    }
  }

  thisPtr.lastX = e.offsetX;
  thisPtr.lastY = e.offsetY;

  if (settings.redrawOnDrag) {
    redrawCanvas(layerdict);
  }
}

function handleMouseWheel(e, layerdict) {
  e.preventDefault();
  e.stopPropagation();
  var t = layerdict.transform;
  var wheeldelta = e.deltaY;
  if (e.deltaMode == 1) {
    // FF only, scroll by lines
    wheeldelta *= 30;
  } else if (e.deltaMode == 2) {
    wheeldelta *= 300;
  }
  var m = Math.pow(1.1, -wheeldelta / 40);
  // Limit amount of zoom per tick.
  if (m > 2) {
    m = 2;
  } else if (m < 0.5) {
    m = 0.5;
  }
  t.zoom *= m;
  var zoomd = (1 - m) / t.zoom;
  t.panx += devicePixelRatio * e.offsetX * zoomd;
  t.pany += devicePixelRatio * e.offsetY * zoomd;
  redrawCanvas(layerdict);
}

function addMouseHandlers(div, layerdict) {
  div.addEventListener("pointerdown", function(e) {
    handlePointerDown(e, layerdict);
  });
  div.addEventListener("pointermove", function(e) {
    handlePointerMove(e, layerdict);
  });
  div.addEventListener("pointerup", function(e) {
    handlePointerUp(e, layerdict);
  });
  var pointerleave = function(e) {
    handlePointerLeave(e, layerdict);
  }
  div.addEventListener("pointercancel", pointerleave);
  div.addEventListener("pointerleave", pointerleave);
  div.addEventListener("pointerout", pointerleave);

  div.onwheel = function(e) {
    handleMouseWheel(e, layerdict);
  }
  for (var element of [div, layerdict.bg, layerdict.fab, layerdict.silk, layerdict.highlight]) {
    element.addEventListener("contextmenu", function(e) {
      e.preventDefault();
    }, false);
  }
}

function setRedrawOnDrag(value) {
  settings.redrawOnDrag = value;
  writeStorage("redrawOnDrag", value);
}

function setBoardRotation(value) {
  settings.boardRotation = value * 5;
  writeStorage("boardRotation", settings.boardRotation);
  document.getElementById("rotationDegree").textContent = settings.boardRotation;
  resizeAll();
}

function initRender() {
  allcanvas = {
    front: {
      transform: {
        x: 0,
        y: 0,
        s: 1,
        panx: 0,
        pany: 0,
        zoom: 1,
      },
      pointerStates: {},
      anotherPointerTapped: false,
      bg: document.getElementById("F_bg"),
      fab: document.getElementById("F_fab"),
      silk: document.getElementById("F_slk"),
      highlight: document.getElementById("F_hl"),
      layer: "F",
    },
    back: {
      transform: {
        x: 0,
        y: 0,
        s: 1,
        panx: 0,
        pany: 0,
        zoom: 1,
      },
      pointerStates: {},
      anotherPointerTapped: false,
      bg: document.getElementById("B_bg"),
      fab: document.getElementById("B_fab"),
      silk: document.getElementById("B_slk"),
      highlight: document.getElementById("B_hl"),
      layer: "B",
    }
  };
  addMouseHandlers(document.getElementById("frontcanvas"), allcanvas.front);
  addMouseHandlers(document.getElementById("backcanvas"), allcanvas.back);
}

///////////////////////////////////////////////

///////////////////////////////////////////////
/*
 * Table reordering via Drag'n'Drop
 * Inspired by: https://htmldom.dev/drag-and-drop-table-column
 */

function setBomHandlers() {

  const bom = document.getElementById('bomtable');

  let dragName;
  let placeHolderElements;
  let draggingElement;
  let forcePopulation;
  let xOffset;
  let yOffset;
  let wasDragged;

  const mouseUpHandler = function(e) {
    // Delete dragging element
    draggingElement.remove();

    // Make BOM selectable again
    bom.style.removeProperty("userSelect");

    // Remove listeners
    document.removeEventListener('mousemove', mouseMoveHandler);
    document.removeEventListener('mouseup', mouseUpHandler);

    if (wasDragged) {
      // Redraw whole BOM
      populateBomTable();
    }
  }

  const mouseMoveHandler = function(e) {
    // Notice the dragging
    wasDragged = true;

    // Make the dragged element visible
    draggingElement.style.removeProperty("display");

    // Set elements position to mouse position
    draggingElement.style.left = `${e.screenX - xOffset}px`;
    draggingElement.style.top = `${e.screenY - yOffset}px`;

    // Forced redrawing of BOM table
    if (forcePopulation) {
      forcePopulation = false;
      // Copy array
      phe = Array.from(placeHolderElements);
      // populate BOM table again
      populateBomHeader(dragName, phe);
      populateBomBody(dragName, phe);
    }

    // Set up array of hidden columns
    var hiddenColumns = Array.from(settings.hiddenColumns);
    // In the ungrouped mode, quantity don't exist
    if (settings.bommode === "ungrouped")
      hiddenColumns.push("Quantity");
    // If no checkbox fields can be found, we consider them hidden
    if (settings.checkboxes.length == 0)
      hiddenColumns.push("checkboxes");

    // Get table headers and group them into checkboxes, extrafields and normal headers
    const bh = document.getElementById("bomhead");
    headers = Array.from(bh.querySelectorAll("th"))
    headers.shift() // numCol is not part of the columnOrder
    headerGroups = []
    lastCompoundClass = null;
    for (i = 0; i < settings.columnOrder.length; i++) {
      cElem = settings.columnOrder[i];
      if (hiddenColumns.includes(cElem)) {
        // Hidden columns appear as a dummy element
        headerGroups.push([]);
        continue;
      }
      elem = headers.filter(e => getColumnOrderName(e) === cElem)[0];
      if (elem.classList.contains("bom-checkbox")) {
        if (lastCompoundClass === "bom-checkbox") {
          cbGroup = headerGroups.pop();
          cbGroup.push(elem);
          headerGroups.push(cbGroup);
        } else {
          lastCompoundClass = "bom-checkbox";
          headerGroups.push([elem])
        }
      } else {
        headerGroups.push([elem])
      }
    }

    // Copy settings.columnOrder
    var columns = Array.from(settings.columnOrder)

    // Set up array with indices of hidden columns
    var hiddenIndices = hiddenColumns.map(e => settings.columnOrder.indexOf(e));
    var dragIndex = columns.indexOf(dragName);
    var swapIndex = dragIndex;
    var swapDone = false;

    // Check if the current dragged element is swapable with the left or right element
    if (dragIndex > 0) {
      // Get left headers boundingbox
      swapIndex = dragIndex - 1;
      while (hiddenIndices.includes(swapIndex) && swapIndex > 0)
        swapIndex--;
      if (!hiddenIndices.includes(swapIndex)) {
        box = getBoundingClientRectFromMultiple(headerGroups[swapIndex]);
        if (e.clientX < box.left + window.scrollX + (box.width / 2)) {
          swapElement = columns[dragIndex];
          columns.splice(dragIndex, 1);
          columns.splice(swapIndex, 0, swapElement);
          forcePopulation = true;
          swapDone = true;
        }
      }
    }
    if ((!swapDone) && dragIndex < headerGroups.length - 1) {
      // Get right headers boundingbox
      swapIndex = dragIndex + 1;
      while (hiddenIndices.includes(swapIndex))
        swapIndex++;
      if (swapIndex < headerGroups.length) {
        box = getBoundingClientRectFromMultiple(headerGroups[swapIndex]);
        if (e.clientX > box.left + window.scrollX + (box.width / 2)) {
          swapElement = columns[dragIndex];
          columns.splice(dragIndex, 1);
          columns.splice(swapIndex, 0, swapElement);
          forcePopulation = true;
          swapDone = true;
        }
      }
    }

    // Write back change to storage
    if (swapDone) {
      settings.columnOrder = columns
      writeStorage("columnOrder", JSON.stringify(columns));
    }

  }

  const mouseDownHandler = function(e) {
    var target = e.target;
    if (target.tagName.toLowerCase() != "td")
      target = target.parentElement;

    // Used to check if a dragging has ever happened
    wasDragged = false;

    // Create new element which will be displayed as the dragged column
    draggingElement = document.createElement("div")
    draggingElement.classList.add("dragging");
    draggingElement.style.display = "none";
    draggingElement.style.position = "absolute";
    draggingElement.style.overflow = "hidden";

    // Get bomhead and bombody elements
    const bh = document.getElementById("bomhead");
    const bb = document.getElementById("bombody");

    // Get all compound headers for the current column
    var compoundHeaders;
    if (target.classList.contains("bom-checkbox")) {
      compoundHeaders = Array.from(bh.querySelectorAll("th.bom-checkbox"));
    } else {
      compoundHeaders = [target];
    }

    // Create new table which will display the column
    var newTable = document.createElement("table");
    newTable.classList.add("bom");
    newTable.style.background = "white";
    draggingElement.append(newTable);

    // Create new header element
    var newHeader = document.createElement("thead");
    newTable.append(newHeader);

    // Set up array for storing all placeholder elements
    placeHolderElements = [];

    // Add all compound headers to the new thead element and placeholders
    compoundHeaders.forEach(function(h) {
      clone = cloneElementWithDimensions(h);
      newHeader.append(clone);
      placeHolderElements.push(clone);
    });

    // Create new body element
    var newBody = document.createElement("tbody");
    newTable.append(newBody);

    // Get indices for compound headers
    var idxs = compoundHeaders.map(e => getBomTableHeaderIndex(e));

    // For each row in the BOM body...
    var rows = bb.querySelectorAll("tr");
    rows.forEach(function(row) {
      // ..get the cells for the compound column
      const tds = row.querySelectorAll("td");
      var copytds = idxs.map(i => tds[i]);
      // Add them to the new element and the placeholders
      var newRow = document.createElement("tr");
      copytds.forEach(function(td) {
        clone = cloneElementWithDimensions(td);
        newRow.append(clone);
        placeHolderElements.push(clone);
      });
      newBody.append(newRow);
    });

    // Compute width for compound header
    var width = compoundHeaders.reduce((acc, x) => acc + x.clientWidth, 0);
    draggingElement.style.width = `${width}px`;

    // Insert the new dragging element and disable selection on BOM
    bom.insertBefore(draggingElement, null);
    bom.style.userSelect = "none";

    // Determine the mouse position offset
    xOffset = e.screenX - compoundHeaders.reduce((acc, x) => Math.min(acc, x.offsetLeft), compoundHeaders[0].offsetLeft);
    yOffset = e.screenY - compoundHeaders[0].offsetTop;

    // Get name for the column in settings.columnOrder
    dragName = getColumnOrderName(target);

    // Change text and class for placeholder elements
    placeHolderElements = placeHolderElements.map(function(e) {
      newElem = cloneElementWithDimensions(e);
      newElem.textContent = "";
      newElem.classList.add("placeholder");
      return newElem;
    });

    // On next mouse move, the whole BOM needs to be redrawn to show the placeholders
    forcePopulation = true;

    // Add listeners for move and up on mouse
    document.addEventListener('mousemove', mouseMoveHandler);
    document.addEventListener('mouseup', mouseUpHandler);
  }

  // In netlist mode, there is nothing to reorder
  if (settings.bommode === "netlist")
    return;

  // Add mouseDownHandler to every column except the numCol
  bom.querySelectorAll("th")
    .forEach(function(head) {
      if (!head.classList.contains("numCol")) {
        head.onmousedown = mouseDownHandler;
      }
    });

}

function getBoundingClientRectFromMultiple(elements) {
  var elems = Array.from(elements);

  if (elems.length == 0)
    return null;

  var box = elems.shift()
    .getBoundingClientRect();

  elems.forEach(function(elem) {
    var elembox = elem.getBoundingClientRect();
    box.left = Math.min(elembox.left, box.left);
    box.top = Math.min(elembox.top, box.top);
    box.width += elembox.width;
    box.height = Math.max(elembox.height, box.height);
  });

  return box;
}

function cloneElementWithDimensions(elem) {
  var newElem = elem.cloneNode(true);
  newElem.style.height = window.getComputedStyle(elem).height;
  newElem.style.width = window.getComputedStyle(elem).width;
  return newElem;
}

function getBomTableHeaderIndex(elem) {
  const bh = document.getElementById('bomhead');
  const ths = Array.from(bh.querySelectorAll("th"));
  return ths.indexOf(elem);
}

function getColumnOrderName(elem) {
  var cname = elem.getAttribute("col_name");
  if (cname === "bom-checkbox")
    return "checkboxes";
  else
    return cname;
}

function resizableGrid(tablehead) {
  var cols = tablehead.firstElementChild.children;
  var rowWidth = tablehead.offsetWidth;

  for (var i = 1; i < cols.length; i++) {
    if (cols[i].classList.contains("bom-checkbox"))
      continue;
    cols[i].style.width = ((cols[i].clientWidth - paddingDiff(cols[i])) * 100 / rowWidth) + '%';
  }

  for (var i = 1; i < cols.length - 1; i++) {
    var div = document.createElement('div');
    div.className = "column-width-handle";
    cols[i].appendChild(div);
    setListeners(div);
  }

  function setListeners(div) {
    var startX, curCol, nxtCol, curColWidth, nxtColWidth, rowWidth;

    div.addEventListener('mousedown', function(e) {
      e.preventDefault();
      e.stopPropagation();

      curCol = e.target.parentElement;
      nxtCol = curCol.nextElementSibling;
      startX = e.pageX;

      var padding = paddingDiff(curCol);

      rowWidth = curCol.parentElement.offsetWidth;
      curColWidth = curCol.clientWidth - padding;
      nxtColWidth = nxtCol.clientWidth - padding;
    });

    document.addEventListener('mousemove', function(e) {
      if (startX) {
        var diffX = e.pageX - startX;
        diffX = -Math.min(-diffX, curColWidth - 20);
        diffX = Math.min(diffX, nxtColWidth - 20);

        curCol.style.width = ((curColWidth + diffX) * 100 / rowWidth) + '%';
        nxtCol.style.width = ((nxtColWidth - diffX) * 100 / rowWidth) + '%';
        console.log(`${curColWidth + nxtColWidth} ${(curColWidth + diffX) * 100 / rowWidth + (nxtColWidth - diffX) * 100 / rowWidth}`);
      }
    });

    document.addEventListener('mouseup', function(e) {
      curCol = undefined;
      nxtCol = undefined;
      startX = undefined;
      nxtColWidth = undefined;
      curColWidth = undefined
    });
  }

  function paddingDiff(col) {

    if (getStyleVal(col, 'box-sizing') == 'border-box') {
      return 0;
    }

    var padLeft = getStyleVal(col, 'padding-left');
    var padRight = getStyleVal(col, 'padding-right');
    return (parseInt(padLeft) + parseInt(padRight));

  }

  function getStyleVal(elm, css) {
    return (window.getComputedStyle(elm, null).getPropertyValue(css))
  }
}

///////////////////////////////////////////////

///////////////////////////////////////////////
/* DOM manipulation and misc code */

var bomsplit;
var canvassplit;
var initDone = false;
var bomSortFunction = null;
var currentSortColumn = null;
var currentSortOrder = null;
var currentHighlightedRowId;
var highlightHandlers = [];
var footprintIndexToHandler = {};
var netsToHandler = {};
var markedFootprints = new Set();
var highlightedFootprints = [];
var highlightedNet = null;
var lastClicked;

function dbg(html) {
  dbgdiv.innerHTML = html;
}

function redrawIfInitDone() {
  if (initDone) {
    redrawCanvas(allcanvas.front);
    redrawCanvas(allcanvas.back);
  }
}

function padsVisible(value) {
  writeStorage("padsVisible", value);
  settings.renderPads = value;
  redrawIfInitDone();
}

function referencesVisible(value) {
  writeStorage("referencesVisible", value);
  settings.renderReferences = value;
  redrawIfInitDone();
}

function valuesVisible(value) {
  writeStorage("valuesVisible", value);
  settings.renderValues = value;
  redrawIfInitDone();
}

function tracksVisible(value) {
  writeStorage("tracksVisible", value);
  settings.renderTracks = value;
  redrawIfInitDone();
}

function zonesVisible(value) {
  writeStorage("zonesVisible", value);
  settings.renderZones = value;
  redrawIfInitDone();
}

function dnpOutline(value) {
  writeStorage("dnpOutline", value);
  settings.renderDnpOutline = value;
  redrawIfInitDone();
}

function setDarkMode(value) {
  if (value) {
    topmostdiv.classList.add("dark");
  } else {
    topmostdiv.classList.remove("dark");
  }
  writeStorage("darkmode", value);
  settings.darkMode = value;
  redrawIfInitDone();
}

function setShowBOMColumn(field, value) {
  if (field === "references") {
    var rl = document.getElementById("reflookup");
    rl.disabled = !value;
    if (!value) {
      rl.value = "";
      updateRefLookup("");
    }
  }

  var n = settings.hiddenColumns.indexOf(field);
  if (value) {
    if (n != -1) {
      settings.hiddenColumns.splice(n, 1);
    }
  } else {
    if (n == -1) {
      settings.hiddenColumns.push(field);
    }
  }

  writeStorage("hiddenColumns", JSON.stringify(settings.hiddenColumns));

  if (initDone) {
    populateBomTable();
  }

  redrawIfInitDone();
}


function setFullscreen(value) {
  if (value) {
    document.documentElement.requestFullscreen();
  } else {
    document.exitFullscreen();
  }
}

function fabricationVisible(value) {
  writeStorage("fabricationVisible", value);
  settings.renderFabrication = value;
  redrawIfInitDone();
}

function silkscreenVisible(value) {
  writeStorage("silkscreenVisible", value);
  settings.renderSilkscreen = value;
  redrawIfInitDone();
}

function setHighlightPin1(value) {
  writeStorage("highlightpin1", value);
  settings.highlightpin1 = value;
  redrawIfInitDone();
}

function getStoredCheckboxRefs(checkbox) {
  function convert(ref) {
    var intref = parseInt(ref);
    if (isNaN(intref)) {
      for (var i = 0; i < pcbdata.footprints.length; i++) {
        if (pcbdata.footprints[i].ref == ref) {
          return i;
        }
      }
      return -1;
    } else {
      return intref;
    }
  }
  if (!(checkbox in settings.checkboxStoredRefs)) {
    var val = readStorage("checkbox_" + checkbox);
    settings.checkboxStoredRefs[checkbox] = val ? val : "";
  }
  if (!settings.checkboxStoredRefs[checkbox]) {
    return new Set();
  } else {
    return new Set(settings.checkboxStoredRefs[checkbox].split(",").map(r => convert(r)).filter(a => a >= 0));
  }
}

function getCheckboxState(checkbox, references) {
  var storedRefsSet = getStoredCheckboxRefs(checkbox);
  var currentRefsSet = new Set(references.map(r => r[1]));
  // Get difference of current - stored
  var difference = new Set(currentRefsSet);
  for (ref of storedRefsSet) {
    difference.delete(ref);
  }
  if (difference.size == 0) {
    // All the current refs are stored
    return "checked";
  } else if (difference.size == currentRefsSet.size) {
    // None of the current refs are stored
    return "unchecked";
  } else {
    // Some of the refs are stored
    return "indeterminate";
  }
}

function setBomCheckboxState(checkbox, element, references) {
  var state = getCheckboxState(checkbox, references);
  element.checked = (state == "checked");
  element.indeterminate = (state == "indeterminate");
}

function createCheckboxChangeHandler(checkbox, references, row) {
  return function () {
    refsSet = getStoredCheckboxRefs(checkbox);
    var markWhenChecked = settings.markWhenChecked == checkbox;
    eventArgs = {
      checkbox: checkbox,
      refs: references,
    }
    if (this.checked) {
      // checkbox ticked
      for (var ref of references) {
        refsSet.add(ref[1]);
      }
      if (markWhenChecked) {
        row.classList.add("checked");
        for (var ref of references) {
          markedFootprints.add(ref[1]);
        }
        drawHighlights();
      }
      eventArgs.state = 'checked';
    } else {
      // checkbox unticked
      for (var ref of references) {
        refsSet.delete(ref[1]);
      }
      if (markWhenChecked) {
        row.classList.remove("checked");
        for (var ref of references) {
          markedFootprints.delete(ref[1]);
        }
        drawHighlights();
      }
      eventArgs.state = 'unchecked';
    }
    settings.checkboxStoredRefs[checkbox] = [...refsSet].join(",");
    writeStorage("checkbox_" + checkbox, settings.checkboxStoredRefs[checkbox]);
    updateCheckboxStats(checkbox);
    EventHandler.emitEvent(IBOM_EVENT_TYPES.CHECKBOX_CHANGE_EVENT, eventArgs);
  }
}

function clearHighlightedFootprints() {
  if (currentHighlightedRowId) {
    document.getElementById(currentHighlightedRowId).classList.remove("highlighted");
    currentHighlightedRowId = null;
    highlightedFootprints = [];
    highlightedNet = null;
  }
}

function createRowHighlightHandler(rowid, refs, net) {
  return function () {
    if (currentHighlightedRowId) {
      if (currentHighlightedRowId == rowid) {
        return;
      }
      document.getElementById(currentHighlightedRowId).classList.remove("highlighted");
    }
    document.getElementById(rowid).classList.add("highlighted");
    currentHighlightedRowId = rowid;
    highlightedFootprints = refs ? refs.map(r => r[1]) : [];
    highlightedNet = net;
    drawHighlights();
    EventHandler.emitEvent(
      IBOM_EVENT_TYPES.HIGHLIGHT_EVENT, {
      rowid: rowid,
      refs: refs,
      net: net
    });
  }
}

function entryMatches(entry) {
  if (settings.bommode == "netlist") {
    // entry is just a net name
    return entry.toLowerCase().indexOf(filter) >= 0;
  }
  // check refs
  if (!settings.hiddenColumns.includes("references")) {
    for (var ref of entry) {
      if (ref[0].toLowerCase().indexOf(filter) >= 0) {
        return true;
      }
    }
  }
  // check fields
  for (var i in config.fields) {
    var f = config.fields[i];
    if (!settings.hiddenColumns.includes(f)) {
      for (var ref of entry) {
        if (pcbdata.bom.fields[ref[1]][i].toLowerCase().indexOf(filter) >= 0) {
          return true;
        }
      }
    }
  }
  return false;
}

function findRefInEntry(entry) {
  return entry.filter(r => r[0].toLowerCase() == reflookup);
}

function highlightFilter(s) {
  if (!filter) {
    return s;
  }
  var parts = s.toLowerCase().split(filter);
  if (parts.length == 1) {
    return s;
  }
  var r = "";
  var pos = 0;
  for (var i in parts) {
    if (i > 0) {
      r += '<mark class="highlight">' +
        s.substring(pos, pos + filter.length) +
        '</mark>';
      pos += filter.length;
    }
    r += s.substring(pos, pos + parts[i].length);
    pos += parts[i].length;
  }
  return r;
}

function checkboxSetUnsetAllHandler(checkboxname) {
  return function () {
    var checkboxnum = 0;
    while (checkboxnum < settings.checkboxes.length &&
      settings.checkboxes[checkboxnum].toLowerCase() != checkboxname.toLowerCase()) {
      checkboxnum++;
    }
    if (checkboxnum >= settings.checkboxes.length) {
      return;
    }
    var allset = true;
    var checkbox;
    var row;
    for (row of bombody.childNodes) {
      checkbox = row.childNodes[checkboxnum + 1].childNodes[0];
      if (!checkbox.checked || checkbox.indeterminate) {
        allset = false;
        break;
      }
    }
    for (row of bombody.childNodes) {
      checkbox = row.childNodes[checkboxnum + 1].childNodes[0];
      checkbox.checked = !allset;
      checkbox.indeterminate = false;
      checkbox.onchange();
    }
  }
}

function createColumnHeader(name, cls, comparator, is_checkbox = false) {
  var th = document.createElement("TH");
  th.innerHTML = name;
  th.classList.add(cls);
  if (is_checkbox)
    th.setAttribute("col_name", "bom-checkbox");
  else
    th.setAttribute("col_name", name);
  var span = document.createElement("SPAN");
  span.classList.add("sortmark");
  span.classList.add("none");
  th.appendChild(span);
  var spacer = document.createElement("div");
  spacer.className = "column-spacer";
  th.appendChild(spacer);
  spacer.onclick = function () {
    if (currentSortColumn && th !== currentSortColumn) {
      // Currently sorted by another column
      currentSortColumn.childNodes[1].classList.remove(currentSortOrder);
      currentSortColumn.childNodes[1].classList.add("none");
      currentSortColumn = null;
      currentSortOrder = null;
    }
    if (currentSortColumn && th === currentSortColumn) {
      // Already sorted by this column
      if (currentSortOrder == "asc") {
        // Sort by this column, descending order
        bomSortFunction = function (a, b) {
          return -comparator(a, b);
        }
        currentSortColumn.childNodes[1].classList.remove("asc");
        currentSortColumn.childNodes[1].classList.add("desc");
        currentSortOrder = "desc";
      } else {
        // Unsort
        bomSortFunction = null;
        currentSortColumn.childNodes[1].classList.remove("desc");
        currentSortColumn.childNodes[1].classList.add("none");
        currentSortColumn = null;
        currentSortOrder = null;
      }
    } else {
      // Sort by this column, ascending order
      bomSortFunction = comparator;
      currentSortColumn = th;
      currentSortColumn.childNodes[1].classList.remove("none");
      currentSortColumn.childNodes[1].classList.add("asc");
      currentSortOrder = "asc";
    }
    populateBomBody();
  }
  if (is_checkbox) {
    spacer.onclick = fancyDblClickHandler(
      spacer, spacer.onclick, checkboxSetUnsetAllHandler(name));
  }
  return th;
}

function populateBomHeader(placeHolderColumn = null, placeHolderElements = null) {
  while (bomhead.firstChild) {
    bomhead.removeChild(bomhead.firstChild);
  }
  var tr = document.createElement("TR");
  var th = document.createElement("TH");
  th.classList.add("numCol");

  var vismenu = document.createElement("div");
  vismenu.id = "vismenu";
  vismenu.classList.add("menu");

  var visbutton = document.createElement("div");
  visbutton.classList.add("visbtn");
  visbutton.classList.add("hideonprint");

  var viscontent = document.createElement("div");
  viscontent.classList.add("menu-content");
  viscontent.id = "vismenu-content";

  settings.columnOrder.forEach(column => {
    if (typeof column !== "string")
      return;

    // Skip empty columns
    if (column === "checkboxes" && settings.checkboxes.length == 0)
      return;
    else if (column === "Quantity" && settings.bommode == "ungrouped")
      return;

    var label = document.createElement("label");
    label.classList.add("menu-label");

    var input = document.createElement("input");
    input.classList.add("visibility_checkbox");
    input.type = "checkbox";
    input.onchange = function (e) {
      setShowBOMColumn(column, e.target.checked)
    };
    input.checked = !(settings.hiddenColumns.includes(column));

    label.appendChild(input);
    if (column.length > 0)
      label.append(column[0].toUpperCase() + column.slice(1));

    viscontent.appendChild(label);
  });

  viscontent.childNodes[0].classList.add("menu-label-top");

  vismenu.appendChild(visbutton);
  if (settings.bommode != "netlist") {
    vismenu.appendChild(viscontent);
    th.appendChild(vismenu);
  }
  tr.appendChild(th);

  var checkboxCompareClosure = function (checkbox) {
    return (a, b) => {
      var stateA = getCheckboxState(checkbox, a);
      var stateB = getCheckboxState(checkbox, b);
      if (stateA > stateB) return -1;
      if (stateA < stateB) return 1;
      return 0;
    }
  }
  var stringFieldCompareClosure = function (fieldIndex) {
    return (a, b) => {
      var fa = pcbdata.bom.fields[a[0][1]][fieldIndex];
      var fb = pcbdata.bom.fields[b[0][1]][fieldIndex];
      if (fa != fb) return fa > fb ? 1 : -1;
      else return 0;
    }
  }
  var referenceRegex = /(?<prefix>[^0-9]+)(?<number>[0-9]+)/;
  var compareRefs = (a, b) => {
    var ra = referenceRegex.exec(a);
    var rb = referenceRegex.exec(b);
    if (ra === null || rb === null) {
      if (a != b) return a > b ? 1 : -1;
      return 0;
    } else {
      if (ra.groups.prefix != rb.groups.prefix) {
        return ra.groups.prefix > rb.groups.prefix ? 1 : -1;
      }
      if (ra.groups.number != rb.groups.number) {
        return parseInt(ra.groups.number) > parseInt(rb.groups.number) ? 1 : -1;
      }
      return 0;
    }
  }
  if (settings.bommode == "netlist") {
    th = createColumnHeader("Net name", "bom-netname", (a, b) => {
      if (a > b) return -1;
      if (a < b) return 1;
      return 0;
    });
    tr.appendChild(th);
  } else {
    // Filter hidden columns
    var columns = settings.columnOrder.filter(e => !settings.hiddenColumns.includes(e));
    var valueIndex = config.fields.indexOf("Value");
    var footprintIndex = config.fields.indexOf("Footprint");
    columns.forEach((column) => {
      if (column === placeHolderColumn) {
        var n = 1;
        if (column === "checkboxes")
          n = settings.checkboxes.length;
        for (i = 0; i < n; i++) {
          td = placeHolderElements.shift();
          tr.appendChild(td);
        }
        return;
      } else if (column === "checkboxes") {
        for (var checkbox of settings.checkboxes) {
          th = createColumnHeader(
            checkbox, "bom-checkbox", checkboxCompareClosure(checkbox), true);
          tr.appendChild(th);
        }
      } else if (column === "References") {
        tr.appendChild(createColumnHeader("References", "references", (a, b) => {
          var i = 0;
          while (i < a.length && i < b.length) {
            if (a[i] != b[i]) return compareRefs(a[i][0], b[i][0]);
            i++;
          }
          return a.length - b.length;
        }));
      } else if (column === "Value") {
        tr.appendChild(createColumnHeader("Value", "value", (a, b) => {
          var ra = a[0][1], rb = b[0][1];
          return valueCompare(
            pcbdata.bom.parsedValues[ra], pcbdata.bom.parsedValues[rb],
            pcbdata.bom.fields[ra][valueIndex], pcbdata.bom.fields[rb][valueIndex]);
        }));
        return;
      } else if (column === "Footprint") {
        tr.appendChild(createColumnHeader(
          "Footprint", "footprint", stringFieldCompareClosure(footprintIndex)));
      } else if (column === "Quantity" && settings.bommode == "grouped") {
        tr.appendChild(createColumnHeader("Quantity", "quantity", (a, b) => {
          return a.length - b.length;
        }));
      } else {
        // Other fields
        var i = config.fields.indexOf(column);
        if (i < 0)
          return;
        tr.appendChild(createColumnHeader(
          column, `field${i + 1}`, stringFieldCompareClosure(i)));
      }
    });
  }
  bomhead.appendChild(tr);
}

function populateBomBody(placeholderColumn = null, placeHolderElements = null) {
  while (bom.firstChild) {
    bom.removeChild(bom.firstChild);
  }
  highlightHandlers = [];
  footprintIndexToHandler = {};
  netsToHandler = {};
  currentHighlightedRowId = null;
  var first = true;
  if (settings.bommode == "netlist") {
    bomtable = pcbdata.nets.slice();
  } else {
    switch (settings.canvaslayout) {
      case 'F':
        bomtable = pcbdata.bom.F.slice();
        break;
      case 'FB':
        bomtable = pcbdata.bom.both.slice();
        break;
      case 'B':
        bomtable = pcbdata.bom.B.slice();
        break;
    }
    if (settings.bommode == "ungrouped") {
      // expand bom table
      expandedTable = []
      for (var bomentry of bomtable) {
        for (var ref of bomentry) {
          expandedTable.push([ref]);
        }
      }
      bomtable = expandedTable;
    }
  }
  if (bomSortFunction) {
    bomtable = bomtable.sort(bomSortFunction);
  }
  for (var i in bomtable) {
    var bomentry = bomtable[i];
    if (filter && !entryMatches(bomentry)) {
      continue;
    }
    var references = null;
    var netname = null;
    var tr = document.createElement("TR");
    var td = document.createElement("TD");
    var rownum = +i + 1;
    tr.id = "bomrow" + rownum;
    td.textContent = rownum;
    tr.appendChild(td);
    if (settings.bommode == "netlist") {
      netname = bomentry;
      td = document.createElement("TD");
      td.innerHTML = highlightFilter(netname ? netname : "&lt;no net&gt;");
      tr.appendChild(td);
    } else {
      if (reflookup) {
        references = findRefInEntry(bomentry);
        if (references.length == 0) {
          continue;
        }
      } else {
        references = bomentry;
      }
      // Filter hidden columns
      var columns = settings.columnOrder.filter(e => !settings.hiddenColumns.includes(e));
      columns.forEach((column) => {
        if (column === placeholderColumn) {
          var n = 1;
          if (column === "checkboxes")
            n = settings.checkboxes.length;
          for (i = 0; i < n; i++) {
            td = placeHolderElements.shift();
            tr.appendChild(td);
          }
          return;
        } else if (column === "checkboxes") {
          for (var checkbox of settings.checkboxes) {
            if (checkbox) {
              td = document.createElement("TD");
              var input = document.createElement("input");
              input.type = "checkbox";
              input.onchange = createCheckboxChangeHandler(checkbox, references, tr);
              setBomCheckboxState(checkbox, input, references);
              if (input.checked && settings.markWhenChecked == checkbox) {
                tr.classList.add("checked");
              }
              td.appendChild(input);
              tr.appendChild(td);
            }
          }
        } else if (column === "References") {
          td = document.createElement("TD");
          td.innerHTML = highlightFilter(references.map(r => r[0]).join(", "));
          tr.appendChild(td);
        } else if (column === "Quantity" && settings.bommode == "grouped") {
          // Quantity
          td = document.createElement("TD");
          td.textContent = references.length;
          tr.appendChild(td);
        } else {
          // All the other fields
          var field_index = config.fields.indexOf(column)
          if (field_index < 0)
            return;
          var valueSet = new Set();
          references.map(r => r[1]).forEach((id) => valueSet.add(pcbdata.bom.fields[id][field_index]));
          td = document.createElement("TD");
          td.innerHTML = highlightFilter(Array.from(valueSet).join(", "));
          tr.appendChild(td);
        }
      });
    }
    bom.appendChild(tr);
    var handler = createRowHighlightHandler(tr.id, references, netname);
    tr.onmousemove = handler;
    highlightHandlers.push({
      id: tr.id,
      handler: handler,
    });
    if (references !== null) {
      for (var refIndex of references.map(r => r[1])) {
        footprintIndexToHandler[refIndex] = handler;
      }
    }
    if (netname !== null) {
      netsToHandler[netname] = handler;
    }
    if ((filter || reflookup) && first) {
      handler();
      first = false;
    }
  }
  EventHandler.emitEvent(
    IBOM_EVENT_TYPES.BOM_BODY_CHANGE_EVENT, {
    filter: filter,
    reflookup: reflookup,
    checkboxes: settings.checkboxes,
    bommode: settings.bommode,
  });
}

function highlightPreviousRow() {
  if (!currentHighlightedRowId) {
    highlightHandlers[highlightHandlers.length - 1].handler();
  } else {
    if (highlightHandlers.length > 1 &&
      highlightHandlers[0].id == currentHighlightedRowId) {
      highlightHandlers[highlightHandlers.length - 1].handler();
    } else {
      for (var i = 0; i < highlightHandlers.length - 1; i++) {
        if (highlightHandlers[i + 1].id == currentHighlightedRowId) {
          highlightHandlers[i].handler();
          break;
        }
      }
    }
  }
  smoothScrollToRow(currentHighlightedRowId);
}

function highlightNextRow() {
  if (!currentHighlightedRowId) {
    highlightHandlers[0].handler();
  } else {
    if (highlightHandlers.length > 1 &&
      highlightHandlers[highlightHandlers.length - 1].id == currentHighlightedRowId) {
      highlightHandlers[0].handler();
    } else {
      for (var i = 1; i < highlightHandlers.length; i++) {
        if (highlightHandlers[i - 1].id == currentHighlightedRowId) {
          highlightHandlers[i].handler();
          break;
        }
      }
    }
  }
  smoothScrollToRow(currentHighlightedRowId);
}

function populateBomTable() {
  populateBomHeader();
  populateBomBody();
  setBomHandlers();
  resizableGrid(bomhead);
}

function footprintsClicked(footprintIndexes) {
  var lastClickedIndex = footprintIndexes.indexOf(lastClicked);
  for (var i = 1; i <= footprintIndexes.length; i++) {
    var refIndex = footprintIndexes[(lastClickedIndex + i) % footprintIndexes.length];
    if (refIndex in footprintIndexToHandler) {
      lastClicked = refIndex;
      footprintIndexToHandler[refIndex]();
      smoothScrollToRow(currentHighlightedRowId);
      break;
    }
  }
}

function netClicked(net) {
  if (net in netsToHandler) {
    netsToHandler[net]();
    smoothScrollToRow(currentHighlightedRowId);
  } else {
    clearHighlightedFootprints();
    highlightedNet = net;
    drawHighlights();
  }
}

function updateFilter(input) {
  filter = input.toLowerCase();
  populateBomTable();
}

function updateRefLookup(input) {
  reflookup = input.toLowerCase();
  populateBomTable();
}

function changeCanvasLayout(layout) {
  document.getElementById("fl-btn").classList.remove("depressed");
  document.getElementById("fb-btn").classList.remove("depressed");
  document.getElementById("bl-btn").classList.remove("depressed");
  switch (layout) {
    case 'F':
      document.getElementById("fl-btn").classList.add("depressed");
      if (settings.bomlayout != "bom-only") {
        canvassplit.collapse(1);
      }
      break;
    case 'B':
      document.getElementById("bl-btn").classList.add("depressed");
      if (settings.bomlayout != "bom-only") {
        canvassplit.collapse(0);
      }
      break;
    default:
      document.getElementById("fb-btn").classList.add("depressed");
      if (settings.bomlayout != "bom-only") {
        canvassplit.setSizes([50, 50]);
      }
  }
  settings.canvaslayout = layout;
  writeStorage("canvaslayout", layout);
  resizeAll();
  changeBomMode(settings.bommode);
}

function populateMetadata() {
  document.getElementById("title").innerHTML = pcbdata.metadata.title;
  document.getElementById("revision").innerHTML = "Rev: " + pcbdata.metadata.revision;
  document.getElementById("company").innerHTML = pcbdata.metadata.company;
  document.getElementById("filedate").innerHTML = pcbdata.metadata.date;
  if (pcbdata.metadata.title != "") {
    document.title = pcbdata.metadata.title + " BOM";
  }
  // Calculate board stats
  var fp_f = 0,
    fp_b = 0,
    pads_f = 0,
    pads_b = 0,
    pads_th = 0;
  for (var i = 0; i < pcbdata.footprints.length; i++) {
    if (pcbdata.bom.skipped.includes(i)) continue;
    var mod = pcbdata.footprints[i];
    if (mod.layer == "F") {
      fp_f++;
    } else {
      fp_b++;
    }
    for (var pad of mod.pads) {
      if (pad.type == "th") {
        pads_th++;
      } else {
        if (pad.layers.includes("F")) {
          pads_f++;
        }
        if (pad.layers.includes("B")) {
          pads_b++;
        }
      }
    }
  }
  document.getElementById("stats-components-front").innerHTML = fp_f;
  document.getElementById("stats-components-back").innerHTML = fp_b;
  document.getElementById("stats-components-total").innerHTML = fp_f + fp_b;
  document.getElementById("stats-groups-front").innerHTML = pcbdata.bom.F.length;
  document.getElementById("stats-groups-back").innerHTML = pcbdata.bom.B.length;
  document.getElementById("stats-groups-total").innerHTML = pcbdata.bom.both.length;
  document.getElementById("stats-smd-pads-front").innerHTML = pads_f;
  document.getElementById("stats-smd-pads-back").innerHTML = pads_b;
  document.getElementById("stats-smd-pads-total").innerHTML = pads_f + pads_b;
  document.getElementById("stats-th-pads").innerHTML = pads_th;
  // Update version string
  document.getElementById("github-link").innerHTML = "InteractiveHtmlBom&nbsp;" +
    /^v\d+\.\d+/.exec(pcbdata.ibom_version)[0];
}

function changeBomLayout(layout) {
  document.getElementById("bom-btn").classList.remove("depressed");
  document.getElementById("lr-btn").classList.remove("depressed");
  document.getElementById("tb-btn").classList.remove("depressed");
  switch (layout) {
    case 'bom-only':
      document.getElementById("bom-btn").classList.add("depressed");
      if (bomsplit) {
        bomsplit.destroy();
        bomsplit = null;
        canvassplit.destroy();
        canvassplit = null;
      }
      document.getElementById("frontcanvas").style.display = "none";
      document.getElementById("backcanvas").style.display = "none";
      document.getElementById("bot").style.height = "";
      break;
    case 'top-bottom':
      document.getElementById("tb-btn").classList.add("depressed");
      document.getElementById("frontcanvas").style.display = "";
      document.getElementById("backcanvas").style.display = "";
      document.getElementById("bot").style.height = "calc(100% - 80px)";
      document.getElementById("bomdiv").classList.remove("split-horizontal");
      document.getElementById("canvasdiv").classList.remove("split-horizontal");
      document.getElementById("frontcanvas").classList.add("split-horizontal");
      document.getElementById("backcanvas").classList.add("split-horizontal");
      if (bomsplit) {
        bomsplit.destroy();
        bomsplit = null;
        canvassplit.destroy();
        canvassplit = null;
      }
      bomsplit = Split(['#bomdiv', '#canvasdiv'], {
        sizes: [50, 50],
        onDragEnd: resizeAll,
        direction: "vertical",
        gutterSize: 5
      });
      canvassplit = Split(['#frontcanvas', '#backcanvas'], {
        sizes: [50, 50],
        gutterSize: 5,
        onDragEnd: resizeAll
      });
      break;
    case 'left-right':
      document.getElementById("lr-btn").classList.add("depressed");
      document.getElementById("frontcanvas").style.display = "";
      document.getElementById("backcanvas").style.display = "";
      document.getElementById("bot").style.height = "calc(100% - 80px)";
      document.getElementById("bomdiv").classList.add("split-horizontal");
      document.getElementById("canvasdiv").classList.add("split-horizontal");
      document.getElementById("frontcanvas").classList.remove("split-horizontal");
      document.getElementById("backcanvas").classList.remove("split-horizontal");
      if (bomsplit) {
        bomsplit.destroy();
        bomsplit = null;
        canvassplit.destroy();
        canvassplit = null;
      }
      bomsplit = Split(['#bomdiv', '#canvasdiv'], {
        sizes: [50, 50],
        onDragEnd: resizeAll,
        gutterSize: 5
      });
      canvassplit = Split(['#frontcanvas', '#backcanvas'], {
        sizes: [50, 50],
        gutterSize: 5,
        direction: "vertical",
        onDragEnd: resizeAll
      });
  }
  settings.bomlayout = layout;
  writeStorage("bomlayout", layout);
  changeCanvasLayout(settings.canvaslayout);
}

function changeBomMode(mode) {
  document.getElementById("bom-grouped-btn").classList.remove("depressed");
  document.getElementById("bom-ungrouped-btn").classList.remove("depressed");
  document.getElementById("bom-netlist-btn").classList.remove("depressed");
  var chkbxs = document.getElementsByClassName("visibility_checkbox");

  switch (mode) {
    case 'grouped':
      document.getElementById("bom-grouped-btn").classList.add("depressed");
      for (var i = 0; i < chkbxs.length; i++) {
        chkbxs[i].disabled = false;
      }
      break;
    case 'ungrouped':
      document.getElementById("bom-ungrouped-btn").classList.add("depressed");
      for (var i = 0; i < chkbxs.length; i++) {
        chkbxs[i].disabled = false;
      }
      break;
    case 'netlist':
      document.getElementById("bom-netlist-btn").classList.add("depressed");
      for (var i = 0; i < chkbxs.length; i++) {
        chkbxs[i].disabled = true;
      }
  }

  writeStorage("bommode", mode);
  if (mode != settings.bommode) {
    settings.bommode = mode;
    bomSortFunction = null;
    currentSortColumn = null;
    currentSortOrder = null;
    clearHighlightedFootprints();
  }
  populateBomTable();
}

function focusFilterField() {
  focusInputField(document.getElementById("filter"));
}

function focusRefLookupField() {
  focusInputField(document.getElementById("reflookup"));
}

function toggleBomCheckbox(bomrowid, checkboxnum) {
  if (!bomrowid || checkboxnum > settings.checkboxes.length) {
    return;
  }
  var bomrow = document.getElementById(bomrowid);
  var checkbox = bomrow.childNodes[checkboxnum].childNodes[0];
  checkbox.checked = !checkbox.checked;
  checkbox.indeterminate = false;
  checkbox.onchange();
}

function checkBomCheckbox(bomrowid, checkboxname) {
  var checkboxnum = 0;
  while (checkboxnum < settings.checkboxes.length &&
    settings.checkboxes[checkboxnum].toLowerCase() != checkboxname.toLowerCase()) {
    checkboxnum++;
  }
  if (!bomrowid || checkboxnum >= settings.checkboxes.length) {
    return;
  }
  var bomrow = document.getElementById(bomrowid);
  var checkbox = bomrow.childNodes[checkboxnum + 1].childNodes[0];
  checkbox.checked = true;
  checkbox.indeterminate = false;
  checkbox.onchange();
}

function setBomCheckboxes(value) {
  writeStorage("bomCheckboxes", value);
  settings.checkboxes = value.split(",").map((e) => e.trim()).filter((e) => e);
  prepCheckboxes();
  populateMarkWhenCheckedOptions();
  setMarkWhenChecked(settings.markWhenChecked);
}

function setMarkWhenChecked(value) {
  writeStorage("markWhenChecked", value);
  settings.markWhenChecked = value;
  markedFootprints.clear();
  for (var ref of (value ? getStoredCheckboxRefs(value) : [])) {
    markedFootprints.add(ref);
  }
  populateBomTable();
  drawHighlights();
}

function prepCheckboxes() {
  var table = document.getElementById("checkbox-stats");
  while (table.childElementCount > 1) {
    table.removeChild(table.lastChild);
  }
  if (settings.checkboxes.length) {
    table.style.display = "";
  } else {
    table.style.display = "none";
  }
  for (var checkbox of settings.checkboxes) {
    var tr = document.createElement("TR");
    var td = document.createElement("TD");
    td.innerHTML = checkbox;
    tr.appendChild(td);
    td = document.createElement("TD");
    td.id = "checkbox-stats-" + checkbox;
    var progressbar = document.createElement("div");
    progressbar.classList.add("bar");
    td.appendChild(progressbar);
    var text = document.createElement("div");
    text.classList.add("text");
    td.appendChild(text);
    tr.appendChild(td);
    table.appendChild(tr);
    updateCheckboxStats(checkbox);
  }
}

function populateMarkWhenCheckedOptions() {
  var container = document.getElementById("markWhenCheckedContainer");

  if (settings.checkboxes.length == 0) {
    container.parentElement.style.display = "none";
    return;
  }

  container.innerHTML = '';
  container.parentElement.style.display = "inline-block";

  function createOption(name, displayName) {
    var id = "markWhenChecked-" + name;

    var div = document.createElement("div");
    div.classList.add("radio-container");

    var input = document.createElement("input");
    input.type = "radio";
    input.name = "markWhenChecked";
    input.value = name;
    input.id = id;
    input.onchange = () => setMarkWhenChecked(name);
    div.appendChild(input);

    // Preserve the selected element when the checkboxes change
    if (name == settings.markWhenChecked) {
      input.checked = true;
    }

    var label = document.createElement("label");
    label.innerHTML = displayName;
    label.htmlFor = id;
    div.appendChild(label);

    container.appendChild(div);
  }
  createOption("", "None");
  for (var checkbox of settings.checkboxes) {
    createOption(checkbox, checkbox);
  }
}

function updateCheckboxStats(checkbox) {
  var checked = getStoredCheckboxRefs(checkbox).size;
  var total = pcbdata.footprints.length - pcbdata.bom.skipped.length;
  var percent = checked * 100.0 / total;
  var td = document.getElementById("checkbox-stats-" + checkbox);
  td.firstChild.style.width = percent + "%";
  td.lastChild.innerHTML = checked + "/" + total + " (" + Math.round(percent) + "%)";
}

function constrain(number, min, max){
  return Math.min(Math.max(parseInt(number), min), max);
}

document.onkeydown = function (e) {
  switch (e.key) {
    case "n":
      if (document.activeElement.type == "text") {
        return;
      }
      if (currentHighlightedRowId !== null) {
        checkBomCheckbox(currentHighlightedRowId, "placed");
        highlightNextRow();
        e.preventDefault();
      }
      break;
    case "ArrowUp":
      highlightPreviousRow();
      e.preventDefault();
      break;
    case "ArrowDown":
      highlightNextRow();
      e.preventDefault();
      break;
    case "ArrowLeft":
    case "ArrowRight":
      if (document.activeElement.type != "text"){
        e.preventDefault();
        let boardRotationElement = document.getElementById("boardRotation")
        settings.boardRotation = parseInt(boardRotationElement.value);  // degrees / 5
        if (e.key == "ArrowLeft"){
            settings.boardRotation += 3;  // 15 degrees
        }
        else{
            settings.boardRotation -= 3;
        }
        settings.boardRotation = constrain(settings.boardRotation, boardRotationElement.min, boardRotationElement.max);
        boardRotationElement.value = settings.boardRotation
        setBoardRotation(settings.boardRotation);
      }
      break;      
    default:
      break;
  }
  if (e.altKey) {
    switch (e.key) {
      case "f":
        focusFilterField();
        e.preventDefault();
        break;
      case "r":
        focusRefLookupField();
        e.preventDefault();
        break;
      case "z":
        changeBomLayout("bom-only");
        e.preventDefault();
        break;
      case "x":
        changeBomLayout("left-right");
        e.preventDefault();
        break;
      case "c":
        changeBomLayout("top-bottom");
        e.preventDefault();
        break;
      case "v":
        changeCanvasLayout("F");
        e.preventDefault();
        break;
      case "b":
        changeCanvasLayout("FB");
        e.preventDefault();
        break;
      case "n":
        changeCanvasLayout("B");
        e.preventDefault();
        break;
      default:
        break;
    }
    if (e.key >= '1' && e.key <= '9') {
      toggleBomCheckbox(currentHighlightedRowId, parseInt(e.key));
      e.preventDefault();
    }
  }
}

function hideNetlistButton() {
  document.getElementById("bom-ungrouped-btn").classList.remove("middle-button");
  document.getElementById("bom-ungrouped-btn").classList.add("right-most-button");
  document.getElementById("bom-netlist-btn").style.display = "none";
}

window.onload = function (e) {
  initUtils();
  initRender();
  initStorage();
  initDefaults();
  cleanGutters();
  populateMetadata();
  dbgdiv = document.getElementById("dbg");
  bom = document.getElementById("bombody");
  bomhead = document.getElementById("bomhead");
  filter = "";
  reflookup = "";
  if (!("nets" in pcbdata)) {
    hideNetlistButton();
  }
  initDone = true;
  setBomCheckboxes(document.getElementById("bomCheckboxes").value);
  // Triggers render
  changeBomLayout(settings.bomlayout);

  // Users may leave fullscreen without touching the checkbox. Uncheck.
  document.addEventListener('fullscreenchange', () => {
    if (!document.fullscreenElement)
      document.getElementById('fullscreenCheckbox').checked = false;
  });
}

window.onresize = resizeAll;
window.matchMedia("print").addListener(resizeAll);

///////////////////////////////////////////////

///////////////////////////////////////////////

///////////////////////////////////////////////
  </script>
</head>

<body>

<div id="topmostdiv" class="topmostdiv">
  <div id="top">
    <div style="float: right; height: 100%;">
      <div class="hideonprint menu" style="float: right; top: 8px;">
        <button class="menubtn"></button>
        <div class="menu-content">
          <label class="menu-label menu-label-top" style="width: calc(50% - 18px)">
            <input id="darkmodeCheckbox" type="checkbox" onchange="setDarkMode(this.checked)">
            Dark mode
          </label><!-- This comment eats space! All of it!
          --><label class="menu-label menu-label-top" style="width: calc(50% - 17px); border-left: 0;">
            <input id="fullscreenCheckbox" type="checkbox" onchange="setFullscreen(this.checked)">
            Full Screen
          </label>
          <label class="menu-label" style="width: calc(50% - 18px)">
            <input id="fabricationCheckbox" type="checkbox" checked onchange="fabricationVisible(this.checked)">
            Fab layer
          </label><!-- This comment eats space! All of it!
          --><label class="menu-label" style="width: calc(50% - 17px); border-left: 0;">
            <input id="silkscreenCheckbox" type="checkbox" checked onchange="silkscreenVisible(this.checked)">
            Silkscreen
          </label>
          <label class="menu-label" style="width: calc(50% - 18px)">
            <input id="referencesCheckbox" type="checkbox" checked onchange="referencesVisible(this.checked)">
            References
          </label><!-- This comment eats space! All of it!
          --><label class="menu-label" style="width: calc(50% - 17px); border-left: 0;">
            <input id="valuesCheckbox" type="checkbox" checked onchange="valuesVisible(this.checked)">
            Values
          </label>
          <div id="tracksAndZonesCheckboxes">
            <label class="menu-label" style="width: calc(50% - 18px)">
              <input id="tracksCheckbox" type="checkbox" checked onchange="tracksVisible(this.checked)">
              Tracks
            </label><!-- This comment eats space! All of it!
            --><label class="menu-label" style="width: calc(50% - 17px); border-left: 0;">
              <input id="zonesCheckbox" type="checkbox" checked onchange="zonesVisible(this.checked)">
              Zones
            </label>
          </div>
          <label class="menu-label" style="width: calc(50% - 18px)">
            <input id="padsCheckbox" type="checkbox" checked onchange="padsVisible(this.checked)">
            Pads
          </label><!-- This comment eats space! All of it!
          --><label class="menu-label" style="width: calc(50% - 17px); border-left: 0;">
            <input id="dnpOutlineCheckbox" type="checkbox" checked onchange="dnpOutline(this.checked)">
            DNP outlined
          </label>
          <label class="menu-label">
            <input id="highlightpin1Checkbox" type="checkbox" onchange="setHighlightPin1(this.checked)">
            Highlight first pin
          </label>
          <label class="menu-label">
            <input id="dragCheckbox" type="checkbox" checked onchange="setRedrawOnDrag(this.checked)">
            Continuous redraw on drag
          </label>
          <label class="menu-label">
            <span>Board rotation</span>
            <span style="float: right"><span id="rotationDegree">0</span>&#176;</span>
            <input id="boardRotation" type="range" min="-36" max="36" value="0" class="slider" oninput="setBoardRotation(this.value)">
          </label>
          <label class="menu-label">
            <div style="margin-left: 5px">Bom checkboxes</div>
            <input id="bomCheckboxes" class="menu-textbox" type=text
                   oninput="setBomCheckboxes(this.value)">
          </label>
          <label class="menu-label">
            <div style="margin-left: 5px">Mark when checked</div>
            <div id="markWhenCheckedContainer"></div>
          </label>
          <label class="menu-label">
            <span class="shameless-plug">
              <span>Created using</span>
              <a id="github-link" target="blank" href="https://github.com/openscopeproject/InteractiveHtmlBom">InteractiveHtmlBom</a>
              <a target="blank" title="Mouse and keyboard help" href="https://github.com/openscopeproject/InteractiveHtmlBom/wiki/Usage#bom-page-mouse-actions" style="text-decoration: none;"><label class="help-link">?</label></a>
            </span>
          </label>
        </div>
      </div>
      <div class="button-container hideonprint"
           style="float: right; position: relative; top: 8px">
        <button id="fl-btn" class="left-most-button" onclick="changeCanvasLayout('F')"
                title="Front only">F
        </button>
        <button id="fb-btn" class="middle-button" onclick="changeCanvasLayout('FB')"
                title="Front and Back">FB
        </button>
        <button id="bl-btn" class="right-most-button" onclick="changeCanvasLayout('B')"
                title="Back only">B
        </button>
      </div>
      <div class="button-container hideonprint"
           style="float: right; position: relative; top: 8px">
        <button id="bom-btn" class="left-most-button" onclick="changeBomLayout('bom-only')"
                title="BOM only"></button>
        <button id="lr-btn" class="middle-button" onclick="changeBomLayout('left-right')"
                title="BOM left, drawings right"></button>
        <button id="tb-btn" class="right-most-button" onclick="changeBomLayout('top-bottom')"
                title="BOM top, drawings bot"></button>
      </div>
      <div class="button-container hideonprint"
           style="float: right; position: relative; top: 8px">
        <button id="bom-grouped-btn" class="left-most-button" onclick="changeBomMode('grouped')"
                title="Grouped BOM"></button>
        <button id="bom-ungrouped-btn" class="middle-button" onclick="changeBomMode('ungrouped')"
                title="Ungrouped BOM"></button>
        <button id="bom-netlist-btn" class="right-most-button" onclick="changeBomMode('netlist')"
                title="Netlist"></button>
      </div>
      <div class="hideonprint menu" style="float: right; top: 8px;">
        <button class="statsbtn"></button>
        <div class="menu-content">
          <table class="stats">
            <tbody>
              <tr>
                <td width="40%">Board stats</td>
                <td>Front</td>
                <td>Back</td>
                <td>Total</td>
              </tr>
              <tr>
                <td>Components</td>
                <td id="stats-components-front">~</td>
                <td id="stats-components-back">~</td>
                <td id="stats-components-total">~</td>
              </tr>
              <tr>
                <td>Groups</td>
                <td id="stats-groups-front">~</td>
                <td id="stats-groups-back">~</td>
                <td id="stats-groups-total">~</td>
              </tr>
              <tr>
                <td>SMD pads</td>
                <td id="stats-smd-pads-front">~</td>
                <td id="stats-smd-pads-back">~</td>
                <td id="stats-smd-pads-total">~</td>
              </tr>
              <tr>
                <td>TH pads</td>
                <td colspan=3 id="stats-th-pads">~</td>
              </tr>
            </tbody>
          </table>
          <table class="stats">
            <col width="40%"/><col />
            <tbody id="checkbox-stats">
              <tr>
                <td colspan=2 style="border-top: 0">Checkboxes</td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
      <div class="hideonprint menu" style="float: right; top: 8px;">
        <button class="iobtn"></button>
        <div class="menu-content">
          <div class="menu-label menu-label-top">
            <div style="margin-left: 5px;">Save board image</div>
            <div class="flexbox">
              <input id="render-save-width" class="menu-textbox" type="text" value="1000" placeholder="Width"
                  style="flex-grow: 1; width: 50px;" oninput="validateSaveImgDimension(this)">
              <span>X</span>
              <input id="render-save-height" class="menu-textbox" type="text" value="1000" placeholder="Height"
                  style="flex-grow: 1; width: 50px;" oninput="validateSaveImgDimension(this)">
            </div>
            <label>
              <input id="render-save-transparent" type="checkbox">
              Transparent background
            </label>
            <div class="flexbox">
              <button class="savebtn" onclick="saveImage('F')">Front</button>
              <button class="savebtn" onclick="saveImage('B')">Back</button>
            </div>
          </div>
          <div class="menu-label">
            <span style="margin-left: 5px;">Config and checkbox state</span>
            <div class="flexbox">
              <button class="savebtn" onclick="saveSettings()">Export</button>
              <button class="savebtn" onclick="loadSettings()">Import</button>
            </div>
          </div>
          <div class="menu-label">
            <span style="margin-left: 5px;">Save bom table as</span>
            <div class="flexbox">
              <button class="savebtn" onclick="saveBomTable('csv')">csv</button>
              <button class="savebtn" onclick="saveBomTable('txt')">txt</button>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div id="fileinfodiv" style="overflow: auto;">
      <table class="fileinfo">
        <tbody>
          <tr>
            <td id="title" class="title" style="width: 70%">
              Title
            </td>
            <td id="revision" class="title" style="width: 30%">
              Revision
            </td>
          </tr>
          <tr>
            <td id="company">
              Company
            </td>
            <td id="filedate">
              Date
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
  <div id="bot" class="split" style="height: calc(100% - 80px)">
    <div id="bomdiv" class="split split-horizontal">
      <div style="width: 100%">
        <input id="reflookup" class="textbox searchbox reflookup hideonprint" type="text" placeholder="Ref lookup"
               oninput="updateRefLookup(this.value)">
        <input id="filter" class="textbox searchbox filter hideonprint" type="text" placeholder="Filter"
               oninput="updateFilter(this.value)">
        <div class="button-container hideonprint" style="float: left; margin: 0;">
          <button id="copy" title="Copy bom table to clipboard"
               onclick="saveBomTable('clipboard')"></button>
        </div>
      </div>
      <div id="dbg"></div>
      <table class="bom" id="bomtable">
        <thead id="bomhead">
        </thead>
        <tbody id="bombody">
        </tbody>
      </table>
    </div>
    <div id="canvasdiv" class="split split-horizontal">
      <div id="frontcanvas" class="split" touch-action="none" style="overflow: hidden">
        <div style="position: relative; width: 100%; height: 100%;">
          <canvas id="F_bg" style="position: absolute; left: 0; top: 0; z-index: 0;"></canvas>
          <canvas id="F_fab" style="position: absolute; left: 0; top: 0; z-index: 1;"></canvas>
          <canvas id="F_slk" style="position: absolute; left: 0; top: 0; z-index: 2;"></canvas>
          <canvas id="F_hl" style="position: absolute; left: 0; top: 0; z-index: 3;"></canvas>
        </div>
      </div>
      <div id="backcanvas" class="split" touch-action="none" style="overflow: hidden">
        <div style="position: relative; width: 100%; height: 100%;">
          <canvas id="B_bg" style="position: absolute; left: 0; top: 0; z-index: 0;"></canvas>
          <canvas id="B_fab" style="position: absolute; left: 0; top: 0; z-index: 1;"></canvas>
          <canvas id="B_slk" style="position: absolute; left: 0; top: 0; z-index: 2;"></canvas>
          <canvas id="B_hl" style="position: absolute; left: 0; top: 0; z-index: 3;"></canvas>
        </div>
      </div>
    </div>
  </div>
</div>

</body>

</html>

