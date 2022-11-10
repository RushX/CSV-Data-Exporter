
# CSV Exporter (Sample)

This project is created with React Js.

After Downloading open main.html to run the Project.

Path to the source code https://github.com/RushX/CSV-Data-Exporter/blob/master/static/js/main.e34372bd.js

Functions and logic


    function apptr() { 
        function downloadcsv(data,type) {
            var csv = Papa.unparse(data);

            var csvData = new Blob([csv], { type: 'text/csv;charset=utf-8;' });
            var csvURL = null;
            if (navigator.msSaveBlob) {
                csvURL = navigator.msSaveBlob(csvData, 'download.csv');
            }
            else {
                csvURL = window.URL.createObjectURL(csvData);
            }

            var tempLink = document.createElement('a');
            tempLink.href = csvURL;
            tempLink.setAttribute('download', type+'.csv');
            tempLink.click();
        }


        let csvarr = []
        let sortedcsv = []
        var add = setInterval(() => {
            fetch('https://random-data-api.com/api/v2/users').then((data) => { return data.json() }).then((data) => {
                let addr = data.address.city + ", " + data.address.street_name + ", " + data.address.street_address;
                document.getElementById('tabody').innerHTML += "<tr><td>" + data["id"] + "</td><td>" + data.first_name + "</td><td>" + data.last_name + "</td><td>" + data.username + "</td><td>" + data.email + "</td><td>" + data.avatar + "</td><td>" + data.gender + "</td><td>" + data.date_of_birth + "</td><td>" + addr + "</td></tr>";
                csvarr.push({ id: data["id"], first_name: data.first_name, last_name: data.last_name, username: data.username, email: data.email, avatar: data.avatar, gender: data.gender, date_of_birth: data.date_of_birth, address: addr })
            });
        }, 1000)

        let i = document.getElementById('stop')
        i.onclick = () => {
            i.innerHTML = "Stopped";
            clearInterval(add);
            console.log(csvarr);
            document.getElementById('stop').hidden = true;
            document.getElementById('expcsv').hidden = false;
            document.getElementById('expsorted').hidden = false;
            document.getElementById('expcsv').onclick = ()=>{downloadcsv(csvarr,"Data")}
            document.getElementById('expsorted').onclick = () => {
                
                sortedcsv =csvarr
                for (Element in sortedcsv) {

                    Element = sortedcsv.sort(function (a, b) {
                        if (a.first_name > b.first_name) {
                            return 1;
                        } else if (a.first_name < b.first_name) {
                            return -1;
                        }
                    });
                }        
                downloadcsv(sortedcsv,"Data_Sorted")
            };





## Authors

- [@RushX](https://www.github.com/RushX)

