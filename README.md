
Passo a passo para configuração do php_cs para linting nop vs code


1. Instalar o PHP CS Fixer
```bash
composer global require friendsofphp/php-cs-fixer
```
2. Verificar se o PHP CS Fixer está instalado corretamente
```bash
php-cs-fixer --version
```
3.  Instalar extensão no vs code
	[php cs fixer ](https://marketplace.visualstudio.com/items?itemName=junstyle.php-cs-fixer)
4. Configurar o PHP CS Fixer no settings.json

> [!TIP]
> Para encontrar o diretório global do composer
> composer global config home


```json
{
"php-cs-fixer.executablePath": "<Path>/vendor/bin/php-cs-fixer.bat",
    "php-cs-fixer.config": "<Path>/vendor/bin/config.php_cs",
    "php-cs-fixer.onsave": true,
    "php-cs-fixer.rules": "@PSR2",
    "php-cs-fixer.allowRisky": false, 
    "php-cs-fixer.pathMode": "override",
    "php-cs-fixer.exclude": [],
    "php-cs-fixer.autoFixByBracket": true,
    "php-cs-fixer.autoFixBySemicolon": false,
    "php-cs-fixer.formatHtml": true,
    "php-cs-fixer.documentFormattingProvider": true,
}
```

5. Na pasta de binários do composer criar o arquivo de configuração do PHP CS Fixer com o nome config.php_cs
```php
<?php

use PhpCsFixer\Config;
use PhpCsFixer\Finder;

$finder = Finder::create()
    ->in(__DIR__)
    ->exclude('vendor');

return (new Config())
    ->setFinder($finder)
    ->setRules([
        '@PSR2' => true,

        'array_indentation' => true,
        'array_syntax' => ['syntax' => 'short'],
        'combine_consecutive_unsets' => true,
        'phpdoc_separation' => true,
        'multiline_whitespace_before_semicolons' => true,

        'single_quote' => false,

        'binary_operator_spaces' => [
            'default' => 'single_space',
            'operators' => ['=>' => 'align', '=' => 'align_single_space_minimal']
        ],

        'blank_line_after_opening_tag' => true,
        'blank_line_before_statement' => [
            'statements' => ['return']
        ],

        'braces' => [
            'allow_single_line_closure' => true,
        ],

        'concat_space' => ['spacing' => 'one'],
        'declare_equal_normalize' => true,
        'function_typehint_space' => true,

        'single_line_comment_style' => ['comment_types' => ['hash']],

        'include' => true,
        'lowercase_cast' => true,

        'no_blank_lines_after_class_opening' => true,
        'no_closing_tag' => true,
        'no_empty_comment' => true,

        'no_extra_blank_lines' => [
            'tokens' => [
                'extra',
                'throw',
                'use',
                'use_trait',
            ],
        ],

        'no_singleline_whitespace_before_semicolons' => true,
        'no_spaces_around_offset' => true,
        'no_whitespace_before_comma_in_array' => true,
        'no_whitespace_in_blank_line' => true,
        'no_trailing_whitespace_in_comment' => true,

        'object_operator_without_whitespace' => true,

        'single_blank_line_before_namespace' => true,
        'space_after_semicolon' => true,
        'ternary_operator_spaces' => true,
        'trim_array_spaces' => true,
        'unary_operator_spaces' => true,
        'whitespace_after_comma_in_array' => true,

        'class_attributes_separation' => true,
    ])
    ->setIndent("\t")
    ->setLineEnding("\n");
```
