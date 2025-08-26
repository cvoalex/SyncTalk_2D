# Understanding Audio Processing in SyncTalk_2D

## Quick Answer to "What is the system doing with audio?"

**The system does NOT process the entire audio file at once.** Instead, it uses a **sliding window approach** where:

1. **Each video frame** is generated from **exactly 16 audio feature frames**
2. **Window center**: The target video frame index ±8 audio frames
3. **High overlap**: ~94% overlap between consecutive windows for smooth transitions
4. **Boundary handling**: Zero-padding when windows extend beyond audio boundaries

## Demonstration

Run the demo script to see exactly how the windowing works:

```bash
python demo_audio_windowing.py
```

## Debug Mode

To see windowing in action during inference, use the debug flag:

```bash
python inference_328.py --debug_windowing --name [your_model] --audio_path [your_audio]
```

This will show:
- Audio processing summary at start
- Window ranges for first/last 5 frames
- Summary of windowing behavior at end

## Key Files

- `AUDIO_WINDOWING_EXPLAINED.md` - Detailed technical explanation
- `demo_audio_windowing.py` - Interactive demonstration
- `utils.py` - Core windowing functions with added documentation
- `inference_328.py` - Main script with debug windowing features

## Why This Approach?

✅ **Memory efficient** - Only small audio chunks in memory  
✅ **Temporal context** - Each frame has local audio context for better lip-sync  
✅ **Streaming capable** - Can process audio incrementally  
✅ **Smooth transitions** - High overlap ensures temporal consistency