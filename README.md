
Este repositório contém ferramentas e scripts de construção para automatizar a construção de pacotes para o [X Binary Package System](https://github.com/void-linux/xbps) (XBPS).


## Visão geral

Pacotes podem ser criados usando o utilitário `xbps-src` deste repositório. Para construir um pacote específico, forneça o nome do pacote como um argumento para `xbps-src`. Pacotes disponíveis podem ser encontrados nos subdiretórios `/srcpkgs`.

Após uma construção bem-sucedida, o pacote resultante é armazenado em `/binpkgs`. Este diretório pode então ser usado como um repositório XBPS para instalação.

Durante a compilação, todos os arquivos de origem são armazenados em `/pkgdir`. Este diretório é expurgado após uma construção bem-sucedida. Se ocorrer um erro, todos os arquivos em `/pkgdir` serão deixados intocados para fins de depuração.


## Criando pacotes

Para cada novo pacote, primeiro um novo diretório deve ser criado em `/srcpkgs`. Então, um arquivo `template` deve ser criado, contendo as instruções de construção e metadados do pacote.

### Metadados do pacote

Variáveis ​​são usadas para definir metadados do pacote:

```sh
pkgname='my-custom-package'
version='1.0'
revision='1'
arch='armv7l'
depends=() # add runtime dependencies here
makedepends=() # add build dependencies here
short_desc='This is my first custom package.'
license='custom'
homepage='https://example.org'
```

### Instruções de construção

As funções são usadas para automatizar a construção de pacotes:

```sh
prepare() {
  # download sources for this package version
}

package() {
  # build the actual package (compile source files to binaries)
}
```

Todos os arquivos no diretório `/pkgdir` serão incluídos no pacote final quando `package()` retornar com sucesso.

### Assinando pacotes

Os pacotes são assinados automaticamente após a construção. Para assinar pacotes, uma chave de assinatura deve ser gerada. Esta chave pode ser gerada com `ssh-keygen` ou `openssl`:

```sh
$ ssh-keygen -t rsa -m PEM -f signkey.pem
```

```sh
$ openssl genrsa -out signkey.pem
```


[Fonte](https://www.reddit.com/r/voidlinux/comments/pe0yvp/creating_packages_for_local_repo/?tl=pt-br)



