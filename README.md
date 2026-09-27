# inventory

Repository untuk project **inventory**.

> Catatan: saat ini repository belum berisi kode aplikasi. Isinya baru konfigurasi
> GitHub Actions untuk integrasi Claude Code. Perbarui bagian di bawah ini
> setiap kali ada folder atau file baru.

## Struktur Project

```
inventory/
├── .github/
│   └── workflows/
│       ├── blank.yml    # Workflow "Claude Code" (versi awal, tanpa show_full_output)
│       └── claude.yml   # Workflow "Claude Code" (dengan show_full_output: "true")
└── README.md            # Dokumentasi project (file ini)
```

### `.github/workflows/`

Folder ini berisi workflow GitHub Actions yang dijalankan otomatis oleh GitHub.

- **`claude.yml`**: menjalankan [Claude Code Action](https://github.com/anthropics/claude-code-action)
  setiap kali ada komentar baru di issue atau di review pull request yang
  mengandung `@claude`. Workflow ini:
  - berjalan di `ubuntu-latest`,
  - melakukan checkout repository (`actions/checkout@v6`),
  - menjalankan `anthropics/claude-code-action@v1` dengan API key dari secret
    `ANTHROPIC_API_KEY`,
  - mengaktifkan `show_full_output` agar log lengkap tampil di Actions,
  - diberi izin tulis untuk `contents`, `pull-requests`, dan `issues` supaya
    Claude bisa membuat branch, commit, dan membalas komentar.

- **`blank.yml`**: isinya hampir sama dengan `claude.yml` (trigger dan job yang
  sama), hanya tanpa opsi `show_full_output`.

  ⚠️ Karena kedua workflow memakai trigger yang sama, setiap komentar `@claude`
  akan menjalankan **dua job sekaligus**. Sebaiknya hapus salah satunya
  (misalnya `blank.yml`) agar tidak ada job ganda.

## Cara Menggunakan Claude

1. Pastikan secret `ANTHROPIC_API_KEY` sudah diatur di
   **Settings → Secrets and variables → Actions**.
2. Tulis komentar di issue atau pull request yang diawali `@claude`, lalu
   tuliskan permintaan Anda.
