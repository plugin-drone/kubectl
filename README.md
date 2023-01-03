# Plugin kubectl para Drone

Este plugin para o Drone, permite que você execute comandos kubectl em sua pipeline. 

* **settings.ignore_errors**: Parametro que quando setado para 1 ignora qualquer erro de execução do comando (não falha o build). Por padrão vem desativado (não ignora erros);
* **settings.kube_config**: Conteúdo do arquivo kubeconfig para acesso ao cluster kubernetes; 
* **settings.cmd**: Comando ou lista de comandos a serem executados.
## Drone Pipeline
```yaml
steps:

- name: kubectl
  image: plugin-drone/kubectl
  settings:
  + ignore_errors: "1"
    kubeconfig: 
      from_secret: kubeconfig
    cmd: 
    - kubectl get nodes
    - kubectl get namepsaces
```
## Executando o plugin manualmente (testar / desenvolver)

```shell
docker run --rm \
  -e PLUGIN_CMD="kubectl get nodes"
  -e PLUGIN_KUBECONFIG="$(cat ~/.kube/config)" \
  -v $(pwd):$(pwd) \
  -w $(pwd) \
  plugin-drone/kubectl
```

## Contribuindo

Este projeto adota a convenção [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/). É imprescindível que seus commits sigam esse padrão. 

Para contribuir com este projeto você precisa:

1. Fazer checkout do projeto;
2. Criar uma branch com a funcionalidade que deseja (`git checkout -b feature/funcionalidade`);
3. Realize o commit de suas alterações (`git commit -m 'feat: Adicionado minha funcionalidade`);
4. Realize o push do seu branch (`git push origin feature/funcionalidade`);
5. Abra um Pull request para merge do seu branch.