[Back To Main](https://github.com/ccabanero/ios-unit-testing-patterns)

#### Description
Example unit tests for Controller class that is composed of a UIButton and uses the Target-Action pattern to handle button events.

#### Code Sample
	#import <XCTest/XCTest.h>
	#import "MyViewController.h"
	
	@interface MyViewControllerTest : XCTestCase
	
	@property (nonatomic, strong) MyViewController *viewControllerUnderTest;
	
	@end
	
	@implementation MyViewControllerTest
	
	- (void)setUp
	{
	    [super setUp];
	    
	    self.viewControllerUnderTest = [[MyViewController alloc] initWithNibName:@"MyViewController" bundle:nil];
	    
	    //load the controller's view hierarchy
	    [self.viewControllerUnderTest performSelectorOnMainThread:@selector(loadView) withObject:nil waitUntilDone:YES];
	    
	    [self.viewControllerUnderTest performSelectorOnMainThread:@selector(viewDidLoad) withObject:nil waitUntilDone:YES];
	}
	
	- (void)tearDown
	{
	    self.viewControllerUnderTest = nil;
	    
	    [super tearDown];
	}
	
	- (void)testViewControllerComposedOfButton {
	    
	    NSArray *subViews = self.viewControllerUnderTest.view.subviews;
	    
	    XCTAssertTrue([subViews containsObject:self.viewControllerUnderTest.button], @"Button not in view hierarchy of ViewController under test");
	}
	
	- (void)testButtonTriggersActionMethod {
	    
	    XCTAssertTrue([self.viewControllerUnderTest.button actionsForTarget:self.viewControllerUnderTest forControlEvent:UIControlEventTouchUpInside], @"button does not trigger action method TouchUpInside");
	}
	
	//continue with application-specific tests of UIButton ...
	
	@end