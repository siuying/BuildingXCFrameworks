build-static:
	xcodebuild build -scheme FooStatic -destination="iOS" -sdk iphoneos -configuration Release SKIP_INSTALL=NO ONLY_ACTIVE_ARCH=NO BUILD_LIBRARIES_FOR_DISTRIBUTION=YES DEFINES_MODULE=YES CONFIGURATION_BUILD_DIR=build/static/iphoneos
	xcodebuild build -scheme FooStatic -destination="iOS Simulator" -sdk iphonesimulator -configuration Release ONLY_ACTIVE_ARCH=NO KIP_INSTALL=NO BUILD_LIBRARIES_FOR_DISTRIBUTION=YES DEFINES_MODULE=YES CONFIGURATION_BUILD_DIR=build/static/iphonesimulator
	xcodebuild build -scheme FooStatic -destination="platform=macOS,variant=Mac Catalyst" -configuration Release ONLY_ACTIVE_ARCH=NO SKIP_INSTALL=NO BUILD_LIBRARIES_FOR_DISTRIBUTION=YES DEFINES_MODULE=YES CONFIGURATION_BUILD_DIR=build/static/maccatalyst

build-dynamic:
	xcodebuild build -scheme Foo -destination="iOS" -sdk iphoneos -configuration Release SKIP_INSTALL=NO ONLY_ACTIVE_ARCH=NO BUILD_LIBRARIES_FOR_DISTRIBUTION=YES DEFINES_MODULE=YES CONFIGURATION_BUILD_DIR=build/dynamic/iphoneos
	xcodebuild build -scheme Foo -destination="iOS Simulator" -sdk iphonesimulator -configuration Release ONLY_ACTIVE_ARCH=NO SKIP_INSTALL=NO BUILD_LIBRARIES_FOR_DISTRIBUTION=YES DEFINES_MODULE=YES CONFIGURATION_BUILD_DIR=build/dynamic/iphonesimulator
	xcodebuild build -scheme Foo -destination="platform=macOS,variant=Mac Catalyst" -configuration Release ONLY_ACTIVE_ARCH=NO SKIP_INSTALL=NO BUILD_LIBRARIES_FOR_DISTRIBUTION=YES DEFINES_MODULE=YES CONFIGURATION_BUILD_DIR=build/dynamic/maccatalyst

framework-static:
	xcodebuild -create-xcframework \
		-library build/static/iphoneos/libFoo.a \
		-headers build/static/iphoneos/usr/local/include \
		-library build/static/iphonesimulator/libFoo.a \
		-headers build/static/iphonesimulator/usr/local/include \
		-library build/static/maccatalyst/libFoo.a \
		-headers build/static/maccatalyst/usr/local/include \
		-output Frameworks/static/Foo.xcframework

framework-dynamic:
	xcodebuild -create-xcframework \
		-framework build/dynamic/iphoneos/Foo.framework \
		-framework build/dynamic/iphonesimulator/Foo.framework \
		-framework build/dynamic/maccatalyst/Foo.framework \
		-output Frameworks/dynamic/Foo.xcframework

all: clean build-static framework-static build-dynamic framework-dynamic

clean:
	rm -rf ./build
	rm -rf ./Frameworks