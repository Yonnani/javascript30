1. Array.prototype.filter()

   1. ```javascript
      const fifteen = inventors.filter(function(inventor) {
         if (inventor.year >= 1500 && inventor.year < 1600) { // inventor.year <= 1599
             return true; // keep it
         }// else {
            // return false;
         //}
      });
      console.log(fifteen);
      console.table(fifteen);
      
      const fifteen = inventors.filter(inventor => (inventor.year >= 1500 && inventor.year < 1600));
      ```

      

2. Array.prototype.map()

   ```javascript
   const fullNames = inventors.map(inventor => inventor.first + inventor.last);
   console.log(fullNames);
   
   const fullNames = inventors.map(inventor => inventor.first + ' ' + inventor.last);
   const fullNames = inventors.map(inventor => `${inventor.first} ${inventor.last}`);
   ```

3. Array.prototype.sort()

   ```javascript
   const ordered = inventors.sort(function (a, b) { //(firstPerson, secondPerson) {
       if (a.year > b.year) {
           return 1;
       } else {
           return -1;
       }
   });
   
   const ordered = inventors.sort((a, b) => a.year > b.year ? 1 : -1);
   ```

4. Array.prototype.reduce()

   ```javascript
   var totalYears = 0;
   for (var i = 0; i < inventors.length; i++) {
       totalYears += inventors[i].year;
   }
   
   const totalYears = inventors.reduce((total, inventor) => {
       return total + (inventor.passed - inventor.year);
   }, 0);
   
   console.log(totalYears);
   ```

5. sort inventors by years lived

   ```javascript
   const oldest = inventors.sort(function (a, b) {
       const lastGuy = a.passed - a.year;
      	const nextGuy = b.passed - b.year;
       return lastGuy > nextGuy ? -1 ; 1;
   });
   ```

6. create a list of boulevards in Parts that contain 'de' anywhere in the name

   ```javascript
   const category = document.querySelector('.mw-category');
   const links = category.querySelectorAll('a');
   const links = [...category.querySelectorAll('a')];
   const links = Array.from(category.querySelectorAll('a'));
   
   const de = links.map(link => link.textContent);
   const de = links
   			.map(link => link.textContent)
   			.filter(streetName => streetName.includes('de');
   ```

7. Sort Exercise

   ```javascript
   const alpha = people.sort(function(lastOne, nextOne) {
       // const parts = lastOne.split(', ');
       const [aLast, aFirst] = lastOne.split(', ');
       const [bLast, bFirst] = nextOne.split(', ');
       return aLast > bLast ? 1 : -1;
   });
   
   const alpha = people.sort((lastOne, nextOne) => {
       // const parts = lastOne.split(', ');
       const [aLast, aFirst] = lastOne.split(', ');
       const [bLast, bFirst] = nextOne.split(', ');
       return aLast > bLast ? 1 : -1;
   });
   
   console.log(alpha);
   ```

8. Reduce Exercise

   ```javascript
   const transportation = data.reduce(function(obj, item) {
       if (!obj[item]) {
           obj[item] = 0;
       }
       obj[item]++;
       return obj;
   }, {});
   
   console.log(transportation);
   ```

