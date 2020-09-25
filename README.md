# Twig(HTML) { guide: lines; }

*A mostly reasonable approach to Twig*

This is a superset of the [Official SensioLabs Twig Standards](http://twig.sensiolabs.org/doc/coding_standards.html).

## Table of Contents

  1. [Tags](#tags)
  1. [Filters](#filters)
  1. [Functions](#functions)
  1. [Tests](#tests)
  1. [Operators](#operators)
  1. [Variables](#variables)
  1. [Blocks](#blocks)
  1. [Comments](#comments)
  1. [Whitespace](#whitespace)
  1. [Commas](#commas)
  1. [Naming conventions](#naming-conventions)
  1. [Resources](#resources)
  1. [Known issues](#known-issues)
  1. [General](#general)

## Tags

**[⬆ back to top](#table-of-contents)**

## Filters

<a name="replace-string-tokens"><a name="2.1"></a>
  - [2.1]() String tokens to be used inside the `replace` filter should be
    marked with percentage signs.

    ```twig
    {# Bad #}
    {{ sidekicks|replace('{{ robin }}', 'Dick Grayson') }}

    {# Good #}
    {{ sidekicks|replace('%robin%', 'Jason Todd') }}
    ```

**[⬆ back to top](#table-of-contents)**

## Functions

**[⬆ back to top](#table-of-contents)**

## Tests

**[⬆ back to top](#table-of-contents)**

## Operators

**[⬆ back to top](#table-of-contents)**

## Variables

**[⬆ back to top](#table-of-contents)**

## Blocks


**[⬆ back to top](#table-of-contents)**

## Comments

**[⬆ back to top](#table-of-contents)**

## Whitespace

  <a name="whitespace--before-blocks"></a><a name="9.1"></a>
  - [9.1](#whitespace--before-blocks) Place 1 space before the leading brace.

    ```twig
    {# Bad #}
    {% set dog={
      'age': '1 year',
      'breed': 'Bernese Mountain Dog',
    } %};

    {# Good #}
    {% set dog = {
      'age': '1 year',
      'breed': 'Bernese Mountain Dog',
    } %};
    ```

  <a name="whitespace--around-keywords"></a><a name="9.2"></a>
  - [9.2](#whitespace--around-keywords) Place 1 space before the opening
    parenthesis in control statements (`if`, `for` etc.). Place no space
    between the argument list and the function name in function calls and
    declarations.

    ```twig
    {# Bad #}
    {% if(isJedi) %}
      {% set enemy = 'sith' %}
    {% endif %}

    {# Good #}
    {% if (isJedi) %}
      {% set enemy = 'sith' %}
    %}

    {# Bad #}
    {{ jedi|default ('Yoda') }}

    {# Good #}
    {{ jedi|default('Yoda') }}
    ```

  <a name="whitespace--infix-ops"></a><a name="9.3"></a>
  - [9.3](#whitespace--infix-ops) Set off operators with spaces.

    ```twig
    {# Bad #}
    {% set x=y+5 %}

    {# Good #}
    {% set x = y + 5 %}
    ```

  <a name="whitespace--newline-at-end"></a><a name="9.4"></a>
  - [9.4](#whitespace--newline-at-end) End files with a single newline
    character.

    ```twig
    {# Bad #}
    {{ stuff }}
    ```

    ```twig
    {# Bad #}
    {{ stuff }}↵
    ↵
    ```

    ```twig
    {# Good #}
    {{ stuff }}↵
    ```

  <a name="whitespace--padded-blocks"></a><a name="9.5"></a>
  - [9.5](#whitespace--padded-blocks) Do not pad your blocks with blank lines.

    ```twig
    {# Bad #}
    {%

      set foo = 'bar'

    %}

    {# Bad #}
    {% if baz %}

      {{ qux }}
    {% elseif %}
      {{ foo }}

    {% endif %}

    {# Good #}
    {% if baz %}
      {{ qux }}
    {% elseif %}
      {{ foo }}
    {% endif %}
    ```

  <a name="whitespace--in-parens"></a><a name="9.6"></a>
  - [9.6](#whitespace--in-parens) Do not add spaces inside parentheses.

    ```twig
    {# Bad #}
    {{ foo|default( 'foo' ) }}

    {# Good #}
    {{ foo|default('foo') }}
    ```

  <a name="whitespace--in-brackets"></a><a name="9.7"></a>
  - [9.7](#whitespace--in-brackets) Do not add spaces inside brackets.

    ```twig
    {# Bad #}
    {% set foo = [ 1, 2, 3 ] %}
    {{ foo.0 }}

    {# Good #}
    {% set foo = [1, 2, 3] %}
    {{ foo.0 }}
    ```

  <a name="whitespace--in-braces"></a><a name="9.10"></a>
  - [9.8](#whitespace--in-braces) Add spaces inside curly braces.

    ```twig
    {# Bad #}
    {% set foo = {clark: 'kent'} %}

    {# Good #}
    {% set foo = { clark: 'kent' } %}
    ```

  <a name="whitespace--max-len"></a><a name="9.9"></a>
  - [9.9](#whitespace--max-len) Avoid having everything in one line.

    > Why? This ensures readability and maintainability.

    ```twig
    {# Bad #}
    {% if victory|default %}{{ congratulations }}{% else %}{{ failure }}{% endif %}

    {# Good #}
    {% if victory|default %}
      {{ congratulations }}
    {% else %}
      {{ failure }}
    {% endif %}
    ```
    
  <a name="whitespace--attibutes"></a><a name="9.10"></a>
  - [9.10](#whitespace--attibutes) Avoid having too much attributes in single line.

    > Why? This ensures readability and maintainability.

    ```twig
    {# Bad #}
    <img loading="lazy" src="{{ placeholderSrc }}" data-srcset="{{ data.srcset }}" data-sizes="auto" alt="{{ data.alt }}" {% if data.width %}width="{{ data.width }}"{% endif %} {% if data.title %}title="{{ data.title }}"{% endif %} class="image__img lazyload">

    {# Good #}
    <img
        loading="lazy"
        src="{{ placeholderSrc }}"
        data-srcset="{{ data.srcset }}"
        data-sizes="auto"
        alt="{{ data.alt }}"
        {% if data.width %}width="{{ data.width }}"{% endif %}
        {% if data.title %}title="{{ data.title }}"{% endif %}
        class="image__img lazyload"
    >
    ```

**[⬆ back to top](#table-of-contents)**

## Commas

<a name="commas--leading-trailing"></a><a name="10.1"></a>
  - [10.1](#commas--leading-trailing) Leading commas: **No.**

    ```twig
    {# Bad #}
    {%
    set story = [
      'once'
    , 'upon'
    , 'a'
    , 'time'
    ]
    %}

    {# Good #}
    {% set story = [
      once,
      upon,
      aTime,
    ]; %}

    {# Bad #}
    {% set hero = {
        'firstName': 'Ada'
      , 'lastName': 'Lovelace'
      , 'birthYear': '1815'
      , 'superPower': 'computers'
    } %}

    {# Good #}
    {% set hero = {
      'firstName': 'Ada',
      'lastName': 'Lovelace',
      'birthYear': '1815',
      'superPower': 'computers'
    } %}
    ```

**[⬆ back to top](#table-of-contents)**

## Naming conventions

**[⬆ back to top](#table-of-contents)**

## Resources

**Tools**

  - [Standalone Twig Linter](https://github.com/asm89/twig-lint)

**[⬆ back to top](#table-of-contents)**

## Known issues

You can use majority of twig functions, but there are some restrictions ins styleguide,  because we use twig js adapter

<a name="known-issues--macro"></a><a name="13.1"></a>
  - [13.1](#known-issues--macro) Include inside macro not working very well. Example:

    ```twig
    {% macro li(item, class, icon) %}
        <li class="pagination__item {{ class }}">
            <a href="{{ item.url }}" class="pagination__link">
                {% include '@icon' with { name: icon } %}
                {{ item.text }}
            </a>
        </li>
    {% endmacro %}

    {{ ul.li(data.item, 'pagination__item--first', 'arrow') }}
    ```
    
    You can fix this issue by sending whole icon component into macro. Example:
    
    ```twig
        {% macro li(item, class, icon) %}
            <li class="pagination__item {{ class }}">
                <a href="{{ item.url }}" class="pagination__link">
                    {{ icon }}
                    {{ item.text }}
                </a>
            </li>
        {% endmacro %}
    
        {% set icon %}
            {% include '@icon' with { name: 'arrow' } %}
        {% endset %}
        {{ ul.li(data.item, 'pagination__item--first', icon) }}
    ```
    
    It's not nice but will work. 

**[⬆ back to top](#table-of-contents)**

## General

<a name="general--if-wrapping"></a><a name="14.1"></a>
  - [14.1](#general--if-wrapping) If data existence is questionable, use twig IF {% if data %}{% endif %}

    ```twig
    {# Bad #}
    <div class="textfield__error">
        {{ data.error }}
    </div>

    {# Bad #}
    <div class="textfield__error">
        {% if data.error %}
            {{ data.error }}
        {% endif %}
    </div> 
    
    {# Good (no unnecessary html) #}
    {% if data.error %}
        <div class="textfield__error">
            {{ data.error }}
        </div>
    {% endif %}
    ```
    
<a name="general--use-data"></a><a name="14.2"></a>
  - [14.2](#general--use-data) Use data.something only if data really comes from back-end and is changeable

    ```twig
    Example if button icon is fixed and admin can't change it.
    
    <button type="button">
        {{ data.text }}
        {% include '@icon' with { name: icon, class: 'button__icon', modifier: '' } %}
    </button>
    ```

**[⬆ back to top](#table-of-contents)**
