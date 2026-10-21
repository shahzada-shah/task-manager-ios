# Architecture

KAZI Tasks is a SwiftUI app for iOS 17 and up. All data lives on the device, shared with the widget extension through an App Group. There is no networking code.

## Shape

```
Views ── intents ──▶ TaskStore ──▶ undo / redo ring (20 snapshots)
                              ──▶ App Group JSON ──▶ Widgets (small, medium, lock screen)
                              ◀── App Intent (complete from a widget)
                              ──▶ local notification (evening sweep)
```

## Layers

| Layer | What it holds |
|---|---|
| **App** | Today (list or timeline, week strip, overdue, backlog, projects), quick-add sheet, task detail with the focus timer, Momentum, Settings. |
| **Store** | `TaskStore`: persistence, the undo and redo ring, smart snooze, the quick-add parser, streak and insights. |
| **Data** | Value-type models (`KZTask`, `KZProject`, `KZBucket`) saved as JSON in the App Group so the widgets read the same data. |
| **System** | WidgetKit (small, medium with interactive complete, lock-screen pill), App Intents, one evening-sweep notification, VoiceOver custom actions. |

## Problems solved

1. **Undo and redo at scale.** A 20-deep snapshot ring. Every mutation goes through it, so undo survives navigation. Snapshots rather than diffs keep it simple, and copying a few hundred value-type tasks is cheap.
2. **Behavioural modelling.** Completion-hour buckets (un-completing decrements the original bucket) and a 14-day weekday histogram feed `insights()`, which returns coach-voice lines rather than charts.
3. **Smart scheduling.** `smartSlot()` picks the earliest day one to six days out with the fewest open tasks. The swipe previews the target weekday before commit, and the toast explains why.
4. **Natural-language quick add.** A regex table reads `!high`, `every day`, times, weekdays and `#project` as you type, and shows what it read before you commit. A typed date wins over the quick picks.
5. **Accessibility.** Rows announce title, project, due date and subtask progress; swipe actions (Complete, Snooze, Flag) are VoiceOver custom actions; the timer announces time remaining.

## Motion

- Springs for screens, sheets and the completion snap; the check draws itself on completion.
- Transform and opacity only. Every infinite loop (Tick's idles, the breathing add button) stops under Reduce Motion.
- The focus timer ends with a double pulse, not a sound.

## Performance targets

- 60 fps scrolling with 500 tasks (`LazyVStack`, flat row views).
- Undo snapshot under 50 ms, insights rebuild under 100 ms, widget refresh under 500 ms.
