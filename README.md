# openfaas-template-static

An OpenFaaS template to serve static content. Inspired from [openfaas-hugo-template](https://github.com/matipan/openfaas-hugo-template)

Using the minimal `scratch` image and running as non-root

## Usage

Create a new empty repository

```bash
git init
```

Pull down the `openfaas-template-static`

```bash
faas-cli template pull https://github.com/frezbo/openfaas-template-static
```

Create a new FaaS project using the template

```bash
faas new --lang static-site --prefix <use an image prefix for the container image> static-site
```

Now `cd` into `static-side` folder and copy over the static contents

```bash
cd static-site
cat <<<EOF > index.html
<html>
This is a static page served by OpenFaas.
</html>
EOF
```

### Hardening

Since this template is based on `scratch` image `readonly_root_filesystem: true` option can be set for the OpenFaaS template.

Eg:

```yaml
version: 1.0
provider:
  name: openfaas
functions:
  static-site:
    lang: static-site
    handler: ./static-site
    image: <prefix>/static-site:latest
    readonly_root_filesystem: true
```

### Deploying

Run `faas-cli up`

```bash
faas-cli up -f static-site.yml
```
