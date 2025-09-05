# Android Profiler SDK

Lightweight Android performance profiler — FPS, jank, memory, startup times, and main-thread load tracking with JSON/CSV reports & overlay.

---

## ✨ Features
- **FPS & Jank Tracking** – Average FPS, p50/p95/p99 frame times, worst frame, jank %, dropped frames.  
- **Refresh-rate aware** – Supports 60/90/120 Hz and adaptive refresh.  
- **Memory Monitor** – Heap usage, allocation rate, GC counts.  
- **Startup Metrics** – Cold/warm app and activity startup to first draw.  
- **Main-thread Load** – Busy % and long tasks without heavy CPU sampling.  
- **Reports & Overlay** – Export JSON/CSV for offline analysis, or show live overlay during dev.  

---

## 🚀 Installation
*(to be updated when you publish to MavenCentral/Jitpack)*  

```gradle
dependencies {
    implementation("com.org:profiler-core:<version>")
}
```

## 🛠️ Usage

```kotlin
class MyApp : Application() {
    override fun onCreate() {
        super.onCreate()
        val config = ProfilerConfig(
            windowMs = 5_000,
            autoAttachFrameMetrics = true,
            autoAttachJank = true
        )
        Profiler.startGlobal(this, config)
    }
}
```

### Start/stop a session manually:
```
val handle = Profiler.fps.startSession("main-flow")
// ... user interaction ...
val stats = Profiler.fps.endSession(handle)
Log.d("Profiler", "Session stats: ${stats.toPrettyJson()}")
```


### Export CSV or JSON:

📊 Example Output
```
{
  "fps": {
    "frames": 382,
    "avgFps": 59.8,
    "p95FrameMs": 21.3,
    "jankPct": 4.2
  },
  "memory": {
    "javaHeapUsedMb": 210,
    "allocRateBytesPerSec": 3200000
  },
  "startup": {
    "kind": "COLD",
    "appStartToFirstDrawMs": 820
  }
}
```

