# Git

Referências oficiais para aprender e consultar Git e GitHub:

- [Livro Pro Git, em português](https://git-scm.com/book/pt-br/v2);
- [Referência dos comandos Git](https://git-scm.com/docs);
- [Instalação do Git](https://git-scm.com/downloads);
- [Documentação do GitHub](https://docs.github.com/pt);
- [Criar um pull request](https://docs.github.com/pt/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request);
- [GitHub Actions](https://docs.github.com/pt/actions);
- [GitHub Container Registry](https://docs.github.com/pt/packages/working-with-a-github-packages-registry/working-with-the-container-registry).

No projeto, o workflow `.github/workflows/deploy.yml` usa Actions para publicar
a imagem do backend no GHCR e implantar por SSH.
