# Kruty1918 Notifications

Gameplay notification queue for Unity: dedup keys, hold durations, FIFO
presentation through an `IGameplayNotificationPresenter` contract, plus a
default TMP/CanvasGroup toast presenter (DOTween-accelerated when available).

## Install (Unity Package Manager)

Package Manager → **+** → **Add package from git URL**:

```
https://github.com/kruty1918dev-ai/com.kruty1918.notifications.git
```

or in `Packages/manifest.json`:

```json
"com.kruty1918.notifications": "https://github.com/kruty1918dev-ai/com.kruty1918.notifications.git#v0.1.0"
```

The repository is private — Git credentials (PAT / Git Credential Manager)
are required on every machine that resolves the package.

## Layout

| Folder | Contents |
|---|---|
| `Runtime/` | Queue service, contracts, default toast presenter |
| `Runtime/API/` | `IGameplayNotificationService`, request/kind contracts |

## API surface

| Type | Purpose |
|---|---|
| `IGameplayNotificationService` | `Show` / `Clear` — enqueue notifications for the player |
| `IGameplayNotificationPresenter` | Presentation seam — swap the default toast for custom UI |
| `GameplayNotificationRequest` | Message + kind + hold duration + dedup key |
| `GameplayNotificationKind` | Info / warning / error-style severities |
| `GameplayNotificationStream` | Static stream so non-DI callers can still publish |

## Model

- Notifications with the same `DedupKey` collapse instead of spamming.
- `HoldDuration` controls how long a notification stays visible.
- The service is engine-agnostic; visuals live behind the presenter contract.

## Dependencies

- `com.unity.ugui` (default presenter uses CanvasGroup/TMP)
