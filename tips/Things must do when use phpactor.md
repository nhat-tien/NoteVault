---
tags:
  - phpactor
date: "2024-03-04"
---

## Disable Diagnostic no used

- Find in source code 
`lib\Extension\WorseReflection\WorseReflectionExtension.php`
- Search for the `registerDiagnosticProviders` method and comment the register of diagnostic provider you want to disable. 
```php
private function registerDiagnosticProviders(ContainerBuilder $container): void
    {
        // $container->register(MissingMemberProvider::class, function (Container $container) {
        //     return new MissingMemberProvider();
        // }, [ self::TAG_DIAGNOSTIC_PROVIDER => []]);
        // $container->register(DocblockMissingReturnTypeProvider::class, function (Container $container) {
        //     return new DocblockMissingReturnTypeProvider();
        // }, [ self::TAG_DIAGNOSTIC_PROVIDER => []]);
        $container->register(DocblockMissingParamProvider::class, function (Container $container) {
            return new DocblockMissingParamProvider();
        }, [ self::TAG_DIAGNOSTIC_PROVIDER => []]);
        $container->register(AssignmentToMissingPropertyProvider::class, function (Container $container) {
            return new AssignmentToMissingPropertyProvider();
        }, [ self::TAG_DIAGNOSTIC_PROVIDER => []]);
        // $container->register(MissingReturnTypeProvider::class, function (Container $container) {
        //     return new MissingReturnTypeProvider();
        // }, [ self::TAG_DIAGNOSTIC_PROVIDER => []]);
        $container->register(UnresolvableNameProvider::class, function (Container $container) {
            return new UnresolvableNameProvider($container->parameter(self::PARAM_IMPORT_GLOBALS)->bool());
        }, [ self::TAG_DIAGNOSTIC_PROVIDER => []]);
```

## Change suggestion variable

`phpactor/lib/Completion/Bridge/TolerantParser/WorseReflection`

`WorseLocalVariableCompletor.php`
```php
public function complete(Node $node, TextDocument $source, ByteOffset $offset): Generator
    {
        if (false === $this->couldComplete($node, $source, $offset)) {
            return true;
        }

        foreach ($this->variableCompletionHelper->variableCompletions($node, $source, $offset) as $local) {
            $localType = $local->type();
            if ($localType instanceof ArrayShapeType) {
                yield from $this->arrayShapeSuggestions($local->name(), $localType);
            }

            yield Suggestion::createWithOptions(
                '$' . $local->name(), // <--- Remove '$'
                [
                    'type' => Suggestion::TYPE_VARIABLE,
                    'short_description' => $this->informationFormatter->format($local),
                    'documentation' => function () use ($local) {
                        return $local->type()->__toString();
                    },
                ]
            );
        }

        return true;
    }
```

## DocblockCompletor

```php
class DocblockCompletor implements TolerantCompletor
{
    const SUPPORTED_TAGS = [
        'property',
        'var',
        'param',
        'return',
        'method',
        'deprecated',
        'extends',
        'implements',
        'template',
        'template-extends',
    ];
    const TAGS_WITH_VAR = [
        'param',
    ];
    const TAGS_WITH_TYPE_ARG = [
        'param',
        'var',
        'return',
        'method',
        'property',
        'implements',
        'extends',
    ];

    public function __construct(
     public function complete(Node $node, TextDocument $source, ByteOffset $byteOffse
            return false;
        }

        // <-- Change here; before: $tag = '@' . $tag;

        if ($var) {
            yield from $this->varCompletion($node, $byteOffset, $tag, $var);
continue;

            }
            yield Suggestion::createWithOptions(
                $parameter->getName(), // <--- Change here; before: '$' . $parameter->getName(),
                [
                    'type' => Suggestion::TYPE_VARIABLE,
                ]
```
