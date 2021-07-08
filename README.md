# Twig & HTML `<guide-lines />`

*A mostly reasonable approach to Twig*

This is a superset of the [Official SensioLabs Twig Standards](https://twig.symfony.com/doc/1.x/coding_standards.html).

## Resources

- [Twig docs](https://twig.symfony.com/doc/1.x/).

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

<a name="default-data-logic"><a name="2.2"></a>
  - [2.2]() Do not use the default filter for default data.

    Default data should come from context. Use default filter for logic only.

    ```twig
    {# Bad #}
    {{ url|default('#') }}

    {# Good #}
    {{ url|default(data.url) }}
    ```

<a name="merge-filter"><a name="2.3"></a>
  - [2.3]() Use merge filter to add to arrays or objects.

    Note that you need to make sure the array/object is iterable.

    ```twig
    {# Bad #}
    {% include '@button' with { data: { text: data.button.text, icon: '#arrow-right' } } %}

    {# Good #}
    {% include '@button' with { data: data.button|merge({ icon: '#arrow-right' }) } %}
    ```

<a name="escape-filter"><a name="2.4"></a>
  - [2.4]() Escape data and values in HTML attributes with the `escape` filter.

    ```twig
    {# Bad #}
    <button data-name="{{ data.name }}">

    {# Good #}
    <button data-name="{{ data.name|escape('html_attr') }}">
    ```

<a name="avoid-filters"><a name="2.5"></a>
  - [2.5]() If possible, avoid transforming data with filters. Transform data beforehand, in PHP.

## Functions

<a name="dump-function"><a name="3.1"></a>
  - [3.1]() Use dump function to debug data.

    Wrap the output with a `pre` tag to make it easier to read.

    ```twig
    <pre>
      {{ dump(user) }}
    </pre>
    ```

## Operators

<a name="do-not-use-math"><a name="4.1"></a>
  - [4.1]() Do not use Math operators.

    Math is calculation logic that should stay in PHP.

    As an example, instead of the mod operator, use batching.
    ```twig
    {# Bad #}
    {% for row in items %}
      {% if loop.index == 1 or (loop.index % 3) == 1 %}
        {# do something with every third item #}
      {% endif %}
    {% endfor %}

    {# Good #}
    {% for row in items|batch(3) %}
      {% for column in row %}
        {% if loop.index == 1 %}
          {# do something with every third item #}
        {% endif %}
      {% endfor %}
    {% endfor %}
    ```


## Variables

<a name="use-set-tags-for-variables"><a name="5.1"></a>
  - [5.1]() Use variables to store common values in templates.

    Instead of doing the same template logic in multiple instances, save the values to variables with `set` tags.

## Comments

<a name="use-set-tags-for-variables"><a name="6.1"></a>
  - [6.1]() Use Twig comments to convey important implementation information to other developers.

    Twig comments will be compiled away, HTML comments are transferred and visible in source to all users.

    ```twig
    {# Bad #}
    <!-- TODO: id should not be static -->
    <input id="input-1" />

    {# Good #}
    {# TODO: id should not be static #}
    <input id="input-1" />
    ```

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
    {% endif %}

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

  <a name="whitespace--attributes"></a><a name="9.10"></a>
  - [9.10](#whitespace--attributes) Avoid having too much attributes in single line.

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

  <a name="whitespace--single-attribute"></a><a name="9.11"></a>
  - [9.11](#whitespace--single-attribute) Avoid having too much logic in a single HTML attribute.

    > Why? This ensures readability and maintainability.

    Instead, split the logic to a separate variable block with whitespace control.

    ```twig
    {# Bad #}
    <div class="textfield{% if modifier %} {{ modifier }}{% endif %}{% if class %} {{ class }}{% endif %}{% if data.isInvalid %} is-invalid{% endif %}{% if data.isDisabled %} is-disabled{% endif %}{% if data.icon %} textfield--icon{% endif %}"></div>

    {# Good #}
    {% set BEM -%}
      textfield
      {% if modifier %} {{ modifier }}{% endif %}
      {%- if class %} {{ class }}{% endif %}
      {%- if data.isInvalid %} is-invalid{% endif %}
      {%- if data.isDisabled %} is-disabled{% endif %}
      {%- if data.icon %} textfield--icon{% endif %}
    {% endset %}
    <div class="{{ BEM }}"></div>
    ```

<a name="whitespace--indenting"></a><a name="9.12"></a>
  - [9.12](#whitespace--indenting) Indenting nested logic and blovks

    For consistency, everything that is nested should be indented by one level more than its context. (Even if it breaks HTML indentation)

    ```twig
    {# Bad #}
    {% if data.title %}
    {{ data.title }}
    {% endif %}

    <div class="row__one">{{ data.rowOne }}</div>
    {% if data.rowTwo %}
    <div class="row__two">{{ data.rowTwo }}</div>
    {% endif %}

    {# Good #}
    {% if data.title %}
        {{ data.title }}
    {% endif %}

    <div class="row__one">{{ data.rowOne }}</div>
    {% if data.rowTwo %}
        <div class="row__two">{{ data.rowTwo }}</div>
    {% endif %}
    ```

## Stylistic rules

<a name="styles--leading-trailing"></a><a name="10.1"></a>
  - [10.1](#styles--leading-trailing) Leading commas: **No.**

    ```twig
    {# Bad #}
    {% set story = [
      'once'
    , 'upon'
    , 'a'
    , 'time'
    ] %}

    {# Good #}
    {% set story = [
      once,
      upon,
      aTime,
    ] %}

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

<a name="styles--quotes"></a><a name="10.2"></a>
  - [10.2](#styles--quotes) Use double quotes for HTML attributes, single quotes for everything else.

    ```twig
    {# Bad #}
    <input value='bad' />

    {# Good #}
    <input value="good" />
    <input value="\"good\"" />

    {# Bad #}
    {% set hero = "bad" %}

    {# Good #}
    {% set hero = 'good' %}
    ```

## Naming conventions

  - [11.1](#naming-camelCase) Use camelCase to name variables.

    ```twig
    {# Bad #}
    {% set story_of_my_life = 'cry baby cry' %}
    {% set storyofmylife = 'cry baby cry' %}

    {# Good #}
    {% set storyOfMyLife = 'cry baby cry' %}
    ```

## Known issues

You can use majority of twig functions, but there are some restrictions in styleguide, because we use Twig.js adapter.

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

## General

<a name="general--twig-php-and-js"><a name="14.1"></a>
  - [14.1]() When deciding to choose whether to use a certain Twig functionality, make sure it is supported by both Twig PHP and [Twig.js](https://github.com/twigjs/twig.js) as we generally use both in our projects.

<a name="general--if-wrapping"></a><a name="14.2"></a>
  - [14.2](#general--if-wrapping) If data existence is questionable, use twig if tag.

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

<a name="general--use-data"></a><a name="14.3"></a>
  - [14.3](#general--use-data) Use data.something only if data really comes from back-end and is changeable

    ```twig
    Example if button icon is fixed and admin can't change it.

    <button type="button">
        {{ data.text }}
        {% include '@icon' with { name: icon, class: 'button__icon', modifier: '' } %}
    </button>
    ```

## HTML

<a name="html--semantics"><a name="15.1"></a>
  - [15.1](#html--semantics) Use semantic [HTML elements](https://developer.mozilla.org/en-US/docs/Web/HTML/Element), wherever appropriate.

    This is to ensure basic usability of the website for all people.

    ```twig
    {# Bad #}
    {# Clickable div that does not have role button nor is tabbable. #}
    <div onclick="">
        {{ data.text }}
    </div>
    <a href="#">this is a button that has interactivity via JS and no real href</a>

    {# Good #}
    <button onclick="">
        {{ data.text }}
    </button>
    <button>this is a button that has interactivity via JS</button>
    ```

<a name="html--landmarks"><a name="15.2"></a>
  - [15.2](#html--landmarks) Use appropriate landmarks to convey important parts of the website to assistive tech.

    See examples in [WAI-ARIA Authoring Practises](https://www.w3.org/TR/wai-aria-practices-1.1/#aria_landmark).


<a name="html--semantic-content-order"><a name="15.3"></a>
  - [15.3](#html--semantic-content-order) Make sure your content order is semantic.

    Sometimes due to design quirks HTML structure cannot be semantically correct. In these cases you can hide the wrongfully placed elements using `aria-hidden="true"` and add visually hidden elements to semantically appropriate places, thus making content order correct and accessible.

    ```twig
    {# Bad #}
    <section>
        <div class="content">...</div>
        <h2>Section title</h2>
        <div class="content">...</div>
    </section>

    {# Better #}
    <section>
        <h2 class="h-visually-hidden">Section title</h2>
        <div class="content">...</div>
        <h2 aria-hidden="true">Section title</h2>
        <div class="content">...</div>
    </section>

    {# Best #}
    {# Work with your designer to make sure the design order follows semantic order! #}
    <section>
        <h2>Section title</h2>
        <div class="content">...</div>
        <div class="content">...</div>
    </section>
    ```

<a name="html--accessibility"><a name="15.4"></a>
  - [15.4](#html--accessibility) Use appropriate ARIA behavior on interactive components that do not exist natively in HTML.

    For example: alerts, dialogs, tooltips, accordions, tabs, autocomplete inputs do not have native HTML elements that convey their behavior and semantics to assistive technology.

    These kinds of interactive components need to have appropriate ARIA roles and JavaScript functionality to work properly for everyone.

    Please explore the [WAI-ARIA Authoring Practises](https://www.w3.org/TR/wai-aria-practices-1.1/) document for specific examples and explanations.

<a name="html--target-blank"><a name="15.5"></a>
  - [15.5](#html--target-blank) Avoid using `target="_blank"` on links.

    Do not force people to new tabs/windows when it is not strictly necessary. People who want to open links in new tabs usually know how to do this themselves.

    See this [CSS-Tricks article](https://css-tricks.com/use-target_blank/) for more explanations.

    If you absolutely must use `target="_blank"` on links, use `rel="noreferrer` with it.
