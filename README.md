# node-cache-action

Composite GitHub Action combining actions/setup-node with actions/cache for node_modules caching.

## Configuration

```yaml
- name: ejson action
  uses: Drafteame/node-cache-action@main
  with:
    node-version: '20' # nodejs version
    working-directory: cmd # path where the npm install command is run.
    cache-key-suffix: suffix # Optional cache key suffix

```

### Outputs

| Output     | Description                                       |
|------------|---------------------------------------------------|
| **cache-path**  | NodeJS modules cache path (node_modules). |
| **cache-key**  | Cache key holding module cache paths. |

## Usage

```yaml
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
        - name: Checkout Repository
        uses: actions/checkout@v4

        - name: ⚙️ Setup NodeJS with cache
        uses: Drafteame/node-cache-action
        with:
            node-version: '20'
            working-directory: cmd/${{ github.event.inputs.service }}
            cache-key-suffix: ${{ github.event.inputs.stage }}
            
      - name: Install SLS dependencies
        working-directory: cmd/${{ github.event.inputs.service }}
        run: npm install
```