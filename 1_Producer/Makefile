build-static:
	xcodebuild build -scheme SampleStatic -destination="iOS" -sdk iphoneos SKIP_INSTALL=NO BUILD_LIBRARIES_FOR_DISTRIBUTION=YES DEFINES_MODULE=YES CONFIGURATION_BUILD_DIR=build/static/iphoneos
	xcodebuild build -scheme SampleStatic -destination="iOS Simulator" -sdk iphonesimulator SKIP_INSTALL=NO BUILD_LIBRARIES_FOR_DISTRIBUTION=YES DEFINES_MODULE=YES CONFIGURATION_BUILD_DIR=build/static/iphonesimulator
	xcodebuild build -scheme SampleStatic -destination="platform=macOS,variant=Mac Catalyst" SKIP_INSTALL=NO BUILD_LIBRARIES_FOR_DISTRIBUTION=YES DEFINES_MODULE=YES CONFIGURATION_BUILD_DIR=build/static/maccatalyst

build-dynamic:
	xcodebuild build -scheme SampleDynamic -destination="iOS" -sdk iphoneos SKIP_INSTALL=NO BUILD_LIBRARIES_FOR_DISTRIBUTION=YES DEFINES_MODULE=YES CONFIGURATION_BUILD_DIR=build/dynamic/iphoneos
	xcodebuild build -scheme SampleDynamic -destination="iOS Simulator" -sdk iphonesimulator SKIP_INSTALL=NO BUILD_LIBRARIES_FOR_DISTRIBUTION=YES DEFINES_MODULE=YES CONFIGURATION_BUILD_DIR=build/dynamic/iphonesimulator
	xcodebuild build -scheme SampleDynamic -destination="platform=macOS,variant=Mac Catalyst" SKIP_INSTALL=NO BUILD_LIBRARIES_FOR_DISTRIBUTION=YES DEFINES_MODULE=YES CONFIGURATION_BUILD_DIR=build/dynamic/maccatalyst

framework-static:
	xcodebuild -create-xcframework \
		-library build/static/iphoneos/libSample.a \
		-headers build/static/iphoneos/usr/local/include \
		-library build/static/iphonesimulator/libSample.a \
		-headers build/static/iphonesimulator/usr/local/include \
		-library build/static/maccatalyst/libSample.a \
		-headers build/static/maccatalyst/usr/local/include \
		-output Frameworks/static/Sample.xcframework

framework-dynamic:
	xcodebuild -create-xcframework \
		-framework build/dynamic/iphoneos/Sample.framework \
		-framework build/dynamic/iphonesimulator/Sample.framework \
		-framework build/dynamic/maccatalyst/Sample.framework \
		-output Frameworks/dynamic/Sample.xcframework

all: clean build-static framework-static build-dynamic framework-dynamic

clean:
	rm -rf ./build
	rm -rf ./Frameworks