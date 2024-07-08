<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="puzzle" content="width=device-width, initial-scale=1.0">
    <title>puzzle!!</title>
    <style>
        .tile{
            width: 70px;
            height: 70px;
            border: 1px solid blue;
            border-radius: 10px;
            text-align: center;
            font-size: 36px;
            background-color: white;
            box-shadow: rgb(128, 128, 128) 5px 5px;
        }
    </style>
    <script>
        "use strict";
        const tiles =[];

        function init(){
            let table = document.getElementById("table");

            for(let i=0; i < 4; i++){
                let tr = document.createElement("tr");

                for(let j = 0; j < 4; j++){
                    let td = document.createElement("td");
                    let index = i * 4 + j;
                    td.className = "tile";
                    td.index = index;
                    td.value = index;
                    td.textContent = index == 0 ? "" : index;
                    td.onclick = click;
                    tr.appendChild(td);
                    tiles.push(td);
                }
                table.appendChild(tr);
            }

            for(let i = 0; i < 1000; i++){
                click({target: {index: Math.floor(Math.random() * 16)}});
            }
        }

        function click(e){
            let i = e.target.index;

            if(i - 4 >= 0 && tiles[i - 4].value == 0){
                swap(i, i - 4);
            }else if(i + 4 < 16 && tiles[i + 4].value == 0){
                swap(i, i + 4);
            }else if(i % 4 != 0 && tiles[i - 1].value == 0){
                swap(i, i - 1);
            }else if(i % 4 != 3 && tiles[i + 1].value == 0){
                swap(i, i + 1);
            }
        }

        function swap(i, j){
            let tmp = tiles[i].textContent;
            tiles[i].textContent = tiles[j].textContent;
            tiles[j].textContent = tmp;
            tmp = tiles[i].value;
            tiles[i].value = tiles[j].value;
            tiles[j].value = tmp;
        }
    </script>
</head>
<body onload="init()">
    <table id="table"></table>
</body>
</html>
