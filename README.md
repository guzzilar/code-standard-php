# PHP Code Standard

Extends from [PSR-1](http://www.php-fig.org/psr/psr-1/), [PSR-2](http://www.php-fig.org/psr/psr-2/)

1. **Comment block, have 1 break line in every tags.**
  
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
     */
    ```
    
    > _**Why?**_  
    > _This approach aimed to increase a readability of a code._  
    > _Think about we have bunch of tags in a DocBlock like below_
    >
    > ```php
    > /**
    >  * This method will send a connection to A.
    >  * Then, observing it and dispatch to B if success.
    >  * @param \Dispatcher $dispatcher
    >  * @param string $code
    >  * @param int $amount
    >  * @param array $params
    >  * @return void
    >  * @throws \DispatchException
    >  * @see http://www.google.com
    >  */
    > public function observer($dispatcher, $code, $amount, $params)
    > {
    >     // ...
    > }
    > ```
    >
    > _The below approach makes code much more easier to read._
    >
    > ```php
    > /**
    >  * This method will send a connection to A.
    >  * Then, observing it and dispatch to B if success.
    >  *
    >  * @param  \Dispatcher $dispatcher
    >  * @param  string      $code
    >  * @param  int         $amount
    >  * @param  array       $params
    >  *
    >  * @return void
    >  *
    >  * @throws \DispatchException
    >  *
    >  * @see    http://www.google.com
    >  */
    > public function observer($dispatcher, $code, $amount, $params)
    > {
    >     // ...
    > }
    > ```

  ---

2. **For any methods in a class, must provide at least a `@param` document if that method is defined an argument unless you use `type-hint`**

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

    > _**Why?**_  
    > _To make other developers easily understand your code since an argument itself cannot tell a type, it could be any of `string`, `int` or even `object`._  
    > _Note, unless you use `type-hint` approach._
    >
    > ```php
    > /**
    >  * This method will send a connection to A.
    >  * Then, observing it and dispatch to B if success.
    >  *
    >  * @return void
    >  *
    >  * @throws \DispatchException
    >  *
    >  * @see    http://www.google.com
    >  */
    > public function observer(
    >     \Dispatcher $dispatcher,
    >     string      $code,
    >     int         $amount,
    >     array       $params
    > ) {
    >     // ...
    > }
    > ```
    
  ---

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
    
    > _**Why?**_  
    > _To increase readability of a code._  

  ---

4. **No shorthand syntax for a conditional block.**
  
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

    > _**Why?**_  
    > _Some of developers implemented with the first style and some of them work with the second style._  
    > _This approach just to make a standard by picking only 1 style._
    >
    > _So, if you want to go with the first style, just go with it for the rest of the code._
    > _Or if you want to go with the second style, just also go with it for your whole project._  
    > _(so I just picked second, to avoid some unintensionally mistake from brackets)._

  ---

5. **Always has 1 breakline at the end of a file.**

  ---

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
    
    > _**Why?**_  
    > _To increase readability of a code._  

  ---

7. **Continue from 5th. If 2 part of code contexts seems different, they don't need to do vertically alignment to each other.**
  
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

    > _**Why?**_  
    > _To increase readability of a code._  

  ---

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

    > _**Why?**_  
    > _To increase readability of a code._  

  ---
  
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

  ---

10. **Use `@test` tag for test method.**
  
    _Hmmm_
    ```php
    public function testCatShouldEatByUsingMouth()
    {
        // ...
    }
    ```
    _Better_
    ```php
    /**
     * @test
     */
    public function cat_should_eat_by_using_mouth()
    {
        // ...
    }
    ```
    
    > _**Why?**_  
    > _To increase readability of a code._  

  ---  

11. **Just use normal-human english sentence style for a test case**
  
    _Hmmm_
    ```php
    /**
     * @test
     */
    public function saySorryIfTicketWasSoldOut()
    {
        // ...
    }
    ```
    _Better_
    ```php
    /**
     * @test
     */
    public function say_sorry_if_ticket_was_sold_out()
    {
        // ...
    }
    ```

  ---

12. **Consider to use [SOLID principle](https://en.wikipedia.org/wiki/SOLID_(object-oriented_design)). Especially, a Single Responsibility principle.**

  ---

13. **Consider to use [Tell, Don't Ask principle](https://pragprog.com/articles/tell-dont-ask)**

  ---

14. **Avoid using `boolean` as one of a parameter.**  
    _added on Mar 2, 2017_

    _Hmmm_
    ```php
    /**
     * @param string $id
     * @param bool   $include_header
     * @param bool   $include_footer
     */
    public function exportData($id, $include_header = false, $include_footer = false)
    {
        // ...
    }
    ```
    _Better_
    ```php
    /**
     * @param string $id
     * @param array  $config
     */
    public function exportData($id, $config = array())
    {
        // ...
    }
    ```
    _Even Better_
    ```php
    class Exporter
    {
        public function __construct(\Template $template)
        {
            // ...
        }

        /**
         * @param string $id
         */
        public function exportData($id)
        {
            $this->template->generate(...);
        }

        // ...
    }
    ```

    > _**Why?**_  
    > _Boolean is not clear enough if you consider from a caller side._  
    > _As from the example above, let's execute it._
    >
    > ```php
    > $exporter = new Exporter;
    > $exporter->exportData('report_id', true, false);
    > ```
    >
    > Now let's assume that you never see the example code before, can you guess an output from the 2nd and 3rd parameters?
    >
    > How about this one,
    >
    > ```php
    > $exporter = new Exporter;
    > $exporter->exportData('report_id', array('includeHeader' => true, 'includeFooter' => false)
    > ```
    >
    > Or even you can go with the 'Even Better' approach.
    >
    > ```php
    > $exporter = new Exporter(Template::include('header', 'footer'));
    > $exporter->exportData('report_id');
    > ```
    >
    > That we can take a responsibility to determine using template out from the Exporter class.
    > Which is we can apply a 'Single Responsibility' principle here.  
    > And since you do dependency injection by passing a Template class. Now you can easily mock a Template class when write a test, or even turn that class to an interface class that you can take-in/out any template you want without any effect to the gathering data part.

    _suggested solution by [@robinclart](https://github.com/robinclart) as from a discussion at [issue#1](https://github.com/guzzilar/code-standard-php/issues/1)_
