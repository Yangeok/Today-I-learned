# 제어문 및 기본문법

- control statement
  - for

    ```php
    // as-is
    <? php
    
    for($i = 0; $i < 10; $i++):
      do_something($i);
    endfor;

    ?>

    // to-be
    <?php for ($i = 0; $i < 10; $i++>): ?>
      <p>Do something in HTML <?php echo $i; ?></p>
    <?php endfor; ?>
    ```

  - foreach

    ```php
    // as-is
    <?php

    foreach ($collection as $item):
      do_something($item);
    endforeach;

    ?>

    // to-be
    <?php foreach ($collection as $item): ?>
      <p>Do something in HTML <?php echo $item; ?></p>
    <?php endforeach; ?>
    ```

  - if/else

    ```php
    // as-is
    <?php
    
    if ($condition):
      do_something();
    elseif ($another_condition):
      do_something_else();
    else:
      do_something_different();
    endif;

    ?>

    // to-be
    <?php if ($condition): ?>
      <p>Do something in HTML</p>
    <?php elseif ($another_condition): ?>
      <p>Do something else in HTML</p>
    <?php else: ?>
      <p>Do something different in HTML</p>
    <?php endif; ?>
    ```

  - switch

    ```php
    // as-is
    <?php

    switch ($condition):
      case $value:
        do_something();
        break();
      default:
        do_something_else();
        break;
    endswitch;

    ?>
    // to-be
    <?php switch ($condition): ?>
    <?php case $value: ?>
      <p>Do something in HTML</p>
      <?php break; ?>
    <?php default: ?>
      <p>Do something else in HTML</p>
      <?php break; ?>
    <?php endswitch; ?>
    ```

  - while

    ```php
    // as-is
    <?php 
    
    while ($condition):
      do_something();
    endwhile;
    
    ?>
    
    // to-be
    <?php while ($condition): ?>
      <p>Do something in HTML</p>
    <?php endwhile; ?>
    ```

- typed php

  ```php
  function foo (int $x) {
    return $x;
  }
  ```

- arrow function

  ```php
  // generally
  $foo = fn (int $x) => $x;

  // using ref to returning value
  fn& ($x) => $x;

  // using ref to parameter
  fn (&$x) => $x;
  ```

- const

  ```php
  const FOO = 'foo';
  ```

- exception

  ```php
  try {
    do_something();
  } catch(Exception $e) {
    echo $e->errorMessage();
  }
  ```

- php
  - type hint
    - callable
      - function
      - anonymous function
      - static method
      - class instance method
      - using `::`
      - using `__invoke()`
    - float
    - resource
    - mixed
