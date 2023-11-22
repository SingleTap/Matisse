[![](https://jitpack.io/v/lwj1994/Matisse.svg)](https://jitpack.io/#lwj1994/Matisse)

# Matisse

fork from https://github.com/zhihu/Matisse

* Order by edit time
* Separate the capture
* Fix crash when loading large image
* Adapt the Result Api


## How to

To get a Git project into your build:
### Step 1. Add the JitPack repository to your build file

Add it in your root build.gradle at the end of repositories:
```
	allprojects {
		repositories {
			...
			maven { url 'https://jitpack.io' }
		}
	}
```

### Step 2. Add the dependency
```
	dependencies {
	        implementation 'com.github.SingleTap:Matisse:${latestVersion}'
	}
```

## Usage
### picker
```
// pickerLauncher
private final ActivityResultLauncher<Intent> pickerLauncher = registerForActivityResult(
        new ActivityResultContracts.StartActivityForResult(),
        new ActivityResultCallback<ActivityResult>() {
            @Override public void onActivityResult(ActivityResult result) {
                if (result.resultCode != Activity.RESULT_OK) {
                  return@registerForActivityResult
                }
                Intent data = result.getData();
                mAdapter.setData(Matisse.obtainResult(data), Matisse.obtainPathResult(data));
                Log.e("OnActivityResult ", String.valueOf(Matisse.obtainOriginalState(data)));
            }
        });

Matisse.from(this)
       .choose(MimeType.ofImage())
       // ....
       .forResult(pickerLauncher);
```


### capture
you can directly call capture
```
// captureLauncher
private final ActivityResultLauncher<Intent> captureLauncher = registerForActivityResult(
        new ActivityResultContracts.StartActivityForResult(),
        new ActivityResultCallback<ActivityResult>() {
            @Override public void onActivityResult(ActivityResult result) {
                if (result.resultCode != Activity.RESULT_OK) {
                  return@registerForActivityResult
                }
                Intent data = result.getData();
                mAdapter.setData(Matisse.obtainResult(data), Matisse.obtainPathResult(data));
                Log.e("OnActivityResult ", String.valueOf(Matisse.obtainOriginalState(data)));
            }
        });

Matisse.from(SampleActivity.this)
       .performCapture(new CaptureStrategy(true, "com.zhihu.matisse.sample.fileprovider", "test"), captureLauncher);
```
