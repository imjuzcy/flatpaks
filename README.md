# flatpaks

A repository of Flatpaks by [imjuzcy](https://github.com/imjuzcy), hosted via GitHub Pages.

## Adding this Repository

To add this Flatpak repository to your system, run:

```sh
flatpak remote-add --if-not-exists imjuzcy-flatpaks \
  https://imjuzcy.github.io/flatpaks/imjuzcy-flatpaks.flatpakrepo
```

Alternatively, download and open the `.flatpakrepo` file:

```sh
flatpak remote-add --if-not-exists imjuzcy-flatpaks imjuzcy-flatpaks.flatpakrepo
```

## Installing Applications

Once the repository is added, you can browse and install applications:

```sh
# List all available applications
flatpak remote-ls imjuzcy-flatpaks

# Install an application
flatpak install imjuzcy-flatpaks <app-id>
```

### Available Applications

| Application | App ID | Description |
|-------------|--------|-------------|
| Hello World | `io.github.imjuzcy.HelloWorld` | A simple Hello World example Flatpak |

## Removing this Repository

```sh
flatpak remote-delete imjuzcy-flatpaks
```

## Contributing

To add a new application to this repository:

1. Fork this repository
2. Create a Flatpak manifest in the `manifests/` directory
   - Name the file `<app-id>.json` (e.g., `io.github.imjuzcy.MyApp.json`)
   - Follow the [Flatpak manifest format](https://docs.flatpak.org/en/latest/manifests.html)
3. Open a pull request

### Manifest Structure

```
manifests/
└── io.github.example.AppName.json   # Flatpak manifest file
```

### Example Manifest

```json
{
  "app-id": "io.github.example.AppName",
  "runtime": "org.freedesktop.Platform",
  "runtime-version": "23.08",
  "sdk": "org.freedesktop.Sdk",
  "command": "app-name",
  "finish-args": [],
  "modules": [
    {
      "name": "app-name",
      "buildsystem": "simple",
      "build-commands": [
        "install -Dm755 app-name.sh /app/bin/app-name"
      ],
      "sources": [
        {
          "type": "script",
          "dest-filename": "app-name.sh",
          "commands": ["echo 'Hello from app-name!'"]
        }
      ]
    }
  ]
}
```

## GPG Signing (Optional)

To enable GPG signing of the repository:

1. Generate a GPG key: `gpg --full-generate-key`
2. Export the private key: `gpg --export-secret-keys --armor <key-id>`
3. Add it as a GitHub Actions secret named `GPG_PRIVATE_KEY`

The published `.flatpakrepo` file will automatically include the public key for verification.

## License

This project is licensed under the [GNU General Public License v3.0](LICENSE).
