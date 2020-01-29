===============
Guia do Usuário
===============

Primeiro, é necessário registrar os getters e setters que serão usados em sua aplicação.

No exemplo abaixo, registraremos um tipo chamado ``boolean``.

Ele aceitará os valores **1, true, "true", "yes" ou "on"** para verdadeiro  e **0, false, "false", "no" ou "off"** para falso.

.. code:: php

   \Cajudev\GetterSetter::register('boolean', [
      'get' => function($value) {
         return $value;
      },
      'set' => function($value) {
         return filter_var($value, FILTER_VALIDATE_BOOLEAN, FILTER_NULL_ON_FAILURE);
      }
   ]);

Esse registro é feito apenas uma vez, e depois poderá será utilizado sempre que você quiser.

Agora iremos desenvolver uma classe de exemplo que usufruirá desse recurso.

.. code:: php

   class Example {
      use \Cajudev\GetterSetterAccessor;

      /** @GetterSetter(boolean) */
      private $bool;
   }

Com isso a cada vez que atribuirmos um valor à variável ``bool``, a validação será automaticamente efetuada.

.. code:: php

   $example = new Example();

   $example->bool = "yes";

   var_dump($example->bool); // true

   $example->bool = "false";

   var_dump($example->bool); // false