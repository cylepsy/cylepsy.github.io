# yaml

> YAML Ain't Markup Language

There are lots of reason to learn about using YAML. ~~Like editing the config file of this blog.~~

## Basic Syntax

There are three types of data structures in YAML:

- **Dictionaries**: Key/value pairs.
- **Arrays/list** A sequence of values.
- **Scalars** : Atomic values.

### Dictionaries

Use **conlon+space** for a key/value pair.

```yaml
animal: pets
```

Equivalent in JS:

```JavaScript
{ animal: 'pets'}
```

Another style in YAML:

```yaml
hash: { name: Steve, foo: bar }
```

Equivalent in JS:

```JavaScript
{hash: { name: 'Steve', foo:'bar' } }
```

### Arrays

A list of words start with hyphen and space form an array

```yaml
- cat
- Dog
- Goldfish
```

Equivalent in JS:

```JavaScript
[ 'Cat', 'Dog', 'Goldfish' ]
```

If a submember of the data structure is an array, indent before it.

```yaml
- - Cat
  - Dog
  - Goldfish
```

Equivalent in JS:

```JavaScript
[['Cat', 'Dog', 'Goldfish' ]]
```
