# PHP Code Standard

Extends from [PSR-1](http://www.php-fig.org/psr/psr-1/), [PSR-2](http://www.php-fig.org/psr/psr-2/)

  1. **Comment block, have 1 break line in every annotations.**
  
      _Hmmm_
      ```php
      /**
       * Description
       * @param string $a
       * @param int $b
       * @return \OmiseObject 
       */
      ```
      _Better_
      ```php
      /**
       * Description
       *
       * @param  string $a
       * @param  int    $b
       *
       * @return \OmiseObject 
      ```

  2. **For any methods in a class, must provide at least a `@param` document if that method is defined an argument**

      _Hmmm_
      ```php
      class A
      {
          public function haveFood($name)
          {
              // ...
          }

          public function pay($amount)
          {
              // ...
          }
      }
      ```
      _Better_
      ```php
      class A
      {
          /**
           * @param string $name
           */
          public function haveFood($name)
          {
              // ...
          }

          /**
           * @param int $amount
           */
          public function pay($amount)
          {
              // ...
          }
      }
      ```

  3. **1 space between `!condition`.**
  
      _Hmmm_
      ```php
      if (!$paid) {
          // ...
      } 
      ```  
      _Better_
      ```php
      if (! $paid) {
          // ...
      } 
      ```

  4. **No shorthand syntax for conditional block.**
  
      _Hmmm_
      ```php
      if (! $paid)
          echo "failed";
      ```
      _Better_
      ```php
      if (! $paid) {
          echo "failed";
      }
      ```
      
  5. **Always has 1 breakline at the end of a file.**

  6. **Formatting code vertically alignment (nice to have)**
  
      _Hmmm_
      ```php
      $person->FirstName = "Chris";                
      $person->Surname = "McGrath";                
      $person->Age = 24;                           
      $person->Occupation = "Software Developer";  
      $person->HomeTown = "Brisbane";
      ```
      _Better_
      ```php
      $person->FirstName  = "Chris"; 
      $person->Surname    = "McGrath"; 
      $person->Age        = 24; 
      $person->Occupation = "Software Developer"; 
      $person->HomeTown   = "Brisbane";
      ```
      _note, example from http://www.codealignment.com/Details.html_

  7. **Continue from 5th. If 2 part of code contexts seems differenct, they don't need to do vertically alignment.**
  
      _Hmmm_
      ```php
      // Init personal information
      $person->FirstName  = "Chris";                
      $person->Surname    = "McGrath";                
      $person->Age        = 24;                           
      $person->Occupation = "Software Developer";  
      $person->HomeTown   = "Brisbane";
      
      // Perform insert record.
      if ($person->save()) {
          $log            = new Logger;
          $log->name      = 'my-log.txt';
          $log->create();
      }
      ```
      _Better_
      ```php
      // Init personal information
      $person->FirstName  = "Chris";                
      $person->Surname    = "McGrath";                
      $person->Age        = 24;                           
      $person->Occupation = "Software Developer";  
      $person->HomeTown   = "Brisbane";
      
      // Perform insert record.
      if ($person->save()) {
          $log       = new Logger;
          $log->name = 'my-log.txt';
          $log->create();
      }

      ```

  8. **1 space for variable string concatenation**
  
      _Hmmm_
      ```php
      $name     = 'Guzzilar';
      $sentence = 'Have a nice day!';

      echo "Hello, ".$name.". ".$sentence;
      // Hello, Guzzilar. Have a nice day!
      ```
      _Better_
      ```php
      $name     = 'Guzzilar';
      $sentence = 'Have a nice day!';

      echo "Hello, " . $name . ". " . $sentence;
      // Hello, Guzzilar. Have a nice day!
      ```
      
  9. **Avoid `getter` and `setter` if those methods do nothing more than serving private property.**

      _Hmmm_
      ```php
      class Acme
      {
          /**
           * @var string
           */
          protected $name = 'Guzzilar';

          /**
           * @var int
           */
          protected $age = 99;

          /**
           * @var string
           */
          protected $occupation = 'Developer';
          
          public function getName()
          {
              return $this->name;
          }

          public function getAge()
          {
              return $this->age;
          }

          public function getOccupation()
          {
              return $this->occupation;
          }

          /**
           * @param string $name
           */
          public function setName($name)
          {
              return $this->name = $name;
          }

          /**
           * @param int $age
           */
          public function setAge($age)
          {
              return $this->age = $age;
          }

          /**
           * @param string $occupation
           */
          public function setOccupation($occupation)
          {
              return $this->occupation = $occupation;
          }
      }
      ```
      _Better_
      ```php
      class Acme
      {
          /**
           * @var string
           */
          protected $name = 'Guzzilar';

          /**
           * @var int
           */
          protected $age = 99;

          /**
           * @var string
           */
          protected $occupation = 'Developer';

          public function getName()
          {
              return $this->name;
          }

          public function getAge()
          {
              return $this->age;
          }

          public function getOccupation()
          {
              return $this->occupation;
          }

          /**
           * @param array $data
           */
          public function updatePersonalInformation($data)
          {
              $this->name       = $data['name'];
              $this->age        = $data['age'];
              $this->occupation = $data['occupation'];
          }
      }
      ```
      _Even Better_
      ```php
      // Rename class name to more expose an information.
      class Person
      {
          /**
           * @var string
           */
          protected $name = 'Guzzilar';

          /**
           * @var int
           */
          protected $age = 99;

          /**
           * @var string
           */
          protected $occupation = 'Developer';

          /**
           * Ask yourself why do we need 'get' information here?
           * What is a use case that requires this method?
           * Is it possible to implement it with 'Tell, Don't Ask' principle or something else?
           */
          public function getName()
          {
              return $this->name;
          }

          public function getAge()
          {
              return $this->age;
          }

          public function getOccupation()
          {
              return $this->occupation;
          }

          /**
           * @param array $data
           */
          public function updateInformation($data)
          {
              $this->name       = $data['name'];
              $this->age        = $data['age'];
              $this->occupation = $data['occupation'];
          }
      }
      ```

  10. **Consider to use [SOLID principle](https://en.wikipedia.org/wiki/SOLID_(object-oriented_design)). Especially, Single Responsibility principle.**

  11. **Consider to use [Tell, Don't Ask principle](https://pragprog.com/articles/tell-dont-ask)**
