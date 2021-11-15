There's an issue when adding a `defaultSource` prop to the `Image` component from the `react-native` library on iOS causes an error.

# Replication steps

1. Install dependencies in this project with `yarn`
2. Start a local server with `yarn start --force-manifest-type=expo-updates`. That flag causes the local server to serve the modern manifest type.
3. Press "i" to open the app in an iOS simulator.
4. I expect to see an image of a plant, but instead I see this error:

```
JSON value '{
    "__packager_asset" = 1;
    height = 718;
    scale = 1;
    uri = "https://d1wp6m56sqw74a.cloudfront.net/~assets/f42d36968b67e046ae764b0fe4f30966";
    width = 828;
}' of type NSMutableDictionary cannot be converted to an image. Only local files or data URIs are supported.

+[ABI43_0_0RCTConvert(Deprecated) UIImage:]
    ABI43_0_0RCTConvert.m:1214
__58-[ABI43_0_0RCTComponentData createPropBlock:isShadowView:]_block_invoke.89
__58-[ABI43_0_0RCTComponentData createPropBlock:isShadowView:]_block_invoke_2.90
__46-[ABI43_0_0RCTComponentData setProps:forView:]_block_invoke
__NSDICTIONARY_IS_CALLING_OUT_TO_A_BLOCK__
-[__NSDictionaryM enumerateKeysAndObjectsWithOptions:usingBlock:]
-[ABI43_0_0RCTComponentData setProps:forView:]
__53-[ABI43_0_0RCTUIManager flushUIBlocksWithCompletion:]_block_invoke
__53-[ABI43_0_0RCTUIManager flushUIBlocksWithCompletion:]_block_invoke.426
_dispatch_call_block_and_release
_dispatch_client_callout
_dispatch_main_queue_callback_4CF
__CFRUNLOOP_IS_SERVICING_THE_MAIN_DISPATCH_QUEUE__
__CFRunLoopRun
CFRunLoopRunSpecific
GSEventRunModal
-[UIApplication _run]
UIApplicationMain
main
start_sim
0x0
0x0
__dso_handle
```

# Observations

1. This problem goes away if you remove the `defaultSource` prop
2. This only appears on iOS for me, when loading the first time or "hard" reloading. If you make a change and let the simulator hot reload, the error goes away.
3. I've never actually seen the default image load, even when the real image is being downloaded.
