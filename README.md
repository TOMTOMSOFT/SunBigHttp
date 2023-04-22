# SunBigHttp
HTTP library for iOS (Objective-C, Swift)


[Objective-C example]

1. download sunbighttp.xcframework.zip 
	- unzip and copy to project folder.
	- add to project.

2. info.plist

	- Add 'App Transport Security Settings'.

	- ex)

		<key>NSAppTransportSecurity</key>
		<dict>
			<key>NSAllowsArbitraryLoads</key>
			<true/>
		</dict>	


3. Usage



	3.1. header import

		#import <sunbighttp/SBHttp.h>



	3.2. GET request

		- (IBAction)btn_get:(id)sender
		{
		    NSString* sURL = @"http://yourdomain-and-port/json/?page=2&city=mycity";
		    NSString* sContentType = @"application/x-www-form-urlencoded";
		    NSDictionary* dicParam = @{
		        @"nickname": @"tester10"
		    };
		    
		    SBHttp* gtk = [[SBHttp alloc] init];
		    [gtk get:sURL withParam:dicParam callback:^(NSError *error, NSData *data){
		        
		        if (error) {
		            NSLog(@"error : %@" , error.description);
		            return ;
		        }
		        
		        if (data != nil) {
		        
		            NSDictionary* json = [NSJSONSerialization
		                                  JSONObjectWithData:data
		                                  options:0 error:&error];
		            
		            NSLog(@"json: %@", json);
		            
		            NSString * result = [json objectForKey:@"result"];
		            if ([result isEqualToString:@"SUCCESS"]) {
		                dispatch_async(dispatch_get_main_queue(), ^{
		                    //self.responseView.text = resultSTR;
		                });
		            }
		 
		        }
		    }];
		}	


	3.3. POST (x-www-form-urlencoded)		


		- (IBAction)btn_post_encoded:(id)sender
		{
		    
		    NSString* sURL = @"http://yourdomain-and-port/json/add1";
		    NSString* sContentType = @"application/x-www-form-urlencoded";
		    NSDictionary* dicParam = @{
		        @"nickname": @"your nickname"
		    };
		    
		    SBHttp* gtk = [[SBHttp alloc] init];
		    [gtk post:sURL withParam:dicParam withAttach:nil contentType:sContentType callback:^(NSError *error, NSData *data) {
		        
		        if (error) {
		            NSLog(@"error : %@" , error.description);
		            return ;
		        }
		        
		        if (data != nil) {
		            NSDictionary* json = [NSJSONSerialization
		                                  JSONObjectWithData:data
		                                  options:0 error:&error];
		            
		            NSLog(@"json: %@", json);
		            
		            NSString * result = [json objectForKey:@"result"];
		            if ([result isEqualToString:@"SUCCESS"]) {
		                dispatch_async(dispatch_get_main_queue(), ^{
		                    //self.responseView.text = resultSTR;
		                });
		            }
		 
		        }
		    }];
		}	

	3.4. POST (JSON)		


		- (IBAction)btn_post_json:(id)sender
		{
		    
		    NSString* sURL = @"http://yourdomain-and-port/json/add1";
		    NSString* sContentType = @"application/json";
		    NSDictionary* dicParam = @{
		        @"nickname": @"your nickname"
		    };
		    
		    SBHttp* gtk = [[SBHttp alloc] init];
		    [gtk post:sURL withParam:dicParam withAttach:nil contentType:sContentType callback:^(NSError *error, NSData *data) {
		        
		        if (error) {
		            NSLog(@"error : %@" , error.description);
		            return ;
		        }
		        
		        if (data != nil) {
		           
		            NSDictionary* json = [NSJSONSerialization
		                                  JSONObjectWithData:data
		                                  options:0 error:&error];
		            
		            NSLog(@"json: %@", json);
		            
		            NSString * result = [json objectForKey:@"result"];
		            if ([result isEqualToString:@"SUCCESS"]) {
		                dispatch_async(dispatch_get_main_queue(), ^{
		                    //self.responseView.text = resultSTR;
		                });
		            }
		 
		        }
		    }];
		}

	3.5. POST (Files)


		- (IBAction)btn_post_files:(id)sender
		{
		    
		    NSString* sURL = @"http://p1.sqlite.co.kr:9103/json/add2";
		    NSString* sContentType = @"application/json";
		    NSDictionary* dicParam = @{
		        @"nickname": @"starzankim"
		    };
		    
		    NSMutableArray* arrImg = [NSMutableArray arrayWithObjects:[UIImage imageNamed:@"koala"], [UIImage imageNamed:@"koala-2"], nil];
		    NSMutableArray* arrNames = [NSMutableArray arrayWithObjects:@"koala.png", @"koala-2.png", nil];
		    
		    NSMutableArray* arrFiles = [NSMutableArray array];
		    for(int i=0; i<[arrImg count]; i++) {
		        UIImage* imgData = [arrImg objectAtIndex:i];
		        NSString* sFilename = [arrNames objectAtIndex:i];
		        
		        NSData* dataFile = UIImageJPEGRepresentation(imgData, 90);
		        NSDictionary* dicItem = @{@"Data": dataFile, @"Filename": sFilename};
		        [arrFiles addObject:dicItem];
		    }
		    
		    SBHttp* gtk = [[SBHttp alloc] init];
		    [gtk post:sURL withParam:dicParam withAttach:arrFiles contentType:sContentType callback:^(NSError *error, NSData *data) {
		        
		        if (error) {
		            NSLog(@"에러 발생 : %@" , error.description);
		            return ;
		        }
		        
		        if (data != nil) {
		        
		            NSDictionary* json = [NSJSONSerialization
		                                  JSONObjectWithData:data
		                                  options:0 error:&error];
		            
		            NSLog(@"json: %@", json);
		            
		            NSString * result = [json objectForKey:@"result"];
		            if ([result isEqualToString:@"SUCCESS"]) {
		                dispatch_async(dispatch_get_main_queue(), ^{
		                    //self.responseView.text = resultSTR;
		                });
		            }
		 
		        }
		    }];
		}


