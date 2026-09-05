# Controle de versão

O código da aplicação e esta documentação ficam em repositórios Git separados:

| Conteúdo | Repositório |
| --- | --- |
| Aplicação | [miklt/pcs3443-2021](https://github.com/miklt/pcs3443-2021) |
| Documentação | [miklt/pcs3443-login](https://github.com/miklt/pcs3443-login) |

Git registra o histórico local dos arquivos; GitHub hospeda os repositórios,
revisões e automações. No projeto da aplicação, pushes na branch `main` que
alterem o backend ou sua infraestrutura podem acionar o workflow de implantação.

## Fluxo básico

```bash
git clone git@github.com:miklt/pcs3443-2021.git
cd pcs3443-2021
git switch -c minha-alteracao
git status
git add caminho/do/arquivo
git commit -m "Descrição objetiva da alteração"
git push -u origin minha-alteracao
```

Abra então um pull request no GitHub. Antes do commit, confira `git diff` e
execute as verificações relacionadas ao componente alterado.

Para conhecer os conceitos e outras formas de autenticação do clone, consulte
as [referências de Git](../referencias/recursos.md).
