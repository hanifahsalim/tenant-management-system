# Tenant Management System

An Android app for managing tenants: add a tenant, view all tenants, see the total rent, and call a tenant. Tenants are saved on the phone using Room.

Built by a group of five for Lab 8: App architecture, Git and App distribution.

## Group members

| Name | Admission No. | GitHub | Pull Request |
|---|---|---|---|
| Andrew Omwenga | 190435 | [Supreme-sudo-sketch](https://github.com/Supreme-sudo-sketch) | [PR #1](https://github.com/hanifahsalim/tenant-management-system/pull/1) |
| Phillip Magachi | 174259 | [magachi69](https://github.com/magachi69) | [PR #2](https://github.com/hanifahsalim/tenant-management-system/pull/2) |
| Barbara Nzisa Malei | 168236 | [Barbaramalei](https://github.com/Barbaramalei) | [PR #3](https://github.com/hanifahsalim/tenant-management-system/pull/3) |
| Stacey Sankok | 168122 | [Sayceee](https://github.com/Sayceee) | [PR #4](https://github.com/hanifahsalim/tenant-management-system/pull/4) |
| Hanifah Salim | 189705 | [hanifahsalim](https://github.com/hanifahsalim) | PR #5 (this README and Release v1.0) |

## Who did what

- Hanifah: project setup, repository, Stage 1 and Stage 6 (README, version 1.0, signed APK, Release)
- Andrew: Stage 2, ViewModel and LiveData (PR #1)
- Phillip: Stage 3, Room data layer (PR #2)
- Barbara: Stage 4, screens connected to the ViewModel (PR #3)
- Stacey: Stage 5, repository and ViewModel connected to Room (PR #4)

## Architecture

The app uses a layered structure. The `ui` layer may use the `data` layer, but the `data` layer never uses the `ui` layer.

```
com.example.tenantmanagementsystemgroupa
├── ui
│   ├── auth        LoginActivity, RegisterActivity
│   ├── main        MainActivity (drawer, toolbar, bottom navigation)
│   ├── dashboard   DashboardFragment
│   ├── tenants     AddTenantFragment, ViewTenantsFragment
│   └── viewmodel   TenantViewModel
└── data
    ├── model       Tenant
    ├── local       TenantDao, TenantDatabase (Room)
    └── repository  TenantRepository
```

- UI: Activities and Fragments with Data Binding and the Navigation Component (Safe Args).
- ViewModel: TenantViewModel exposes LiveData to the screens and saves through the repository.
- Repository: TenantRepository is the single place the ViewModel gets tenant data from.
- Database: Room stores tenants on the phone so they remain after the app is closed.

## Git workflow

- The default branch is master and it is protected: changes go in through pull requests that need one approval.
- Each member worked on their own feature branch and a different member reviewed and merged the pull request.

## Run the app

1. Clone the repository: `git clone https://github.com/hanifahsalim/tenant-management-system.git`
2. Open it in Android Studio and wait for Gradle to sync.
3. Run on an emulator or a phone.

## Release

Version 1.0 with the signed APK is on the [Releases page](https://github.com/hanifahsalim/tenant-management-system/releases).

## ViewModel design (Andrew)

- TenantViewModel is in ui.viewmodel and is shared by the screens with activityViewModels().
- It exposes the tenant list as LiveData and three transformed texts using map: tenantCountText, totalRentText and allTenantsText.
- addTenant() trims and validates the input, and returns null when a field is empty.
