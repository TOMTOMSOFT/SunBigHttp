# SunBigHttp
HTTP library for iOS (Objective-C, Swift)


[Objective-C example]

1. download sunbighttp.xcframework.zip 
	- unzip and copy to project folder.
	- add to project.

2. info.plist

	- Add 'App Transport Security Settings'.

	- ex)

~~~
		<key>NSAppTransportSecurity</key>
		<dict>
			<key>NSAllowsArbitraryLoads</key>
			<true/>
		</dict>	
~~~

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

		- HTML 
		<input type="file" name="file1">
		<input type="file" name="file2">


		- (IBAction)btn_post_files:(id)sender
		{
		    
		    NSString* sURL = @"http://p1.sqlite.co.kr:9103/json/add2";
		    NSString* sContentType = @"application/json";
		    NSDictionary* dicParam = @{
		        @"nickname": @"your nickname"
		    };
		    
		    NSMutableArray* arrImg = [NSMutableArray arrayWithObjects:[UIImage imageNamed:@"koala"], [UIImage imageNamed:@"koala-2"], nil];
		    NSMutableArray* arrNames = [NSMutableArray arrayWithObjects:@"koala.png", @"koala-2.png", nil];
		    
		    NSMutableArray* arrFiles = [NSMutableArray array];
		    for(int i=0; i<[arrImg count]; i++) {
		        UIImage* imgData = [arrImg objectAtIndex:i];
		        NSString* sFilename = [arrNames objectAtIndex:i];
			NSString* sKeyName = [NSString stringWithFormat:"file%d", i+1];
		        
		        NSData* dataFile = UIImageJPEGRepresentation(imgData, 1.0);
		        NSDictionary* dicItem = @{@"Data": dataFile, @"Filename": sFilename, @"Name": sKeyName};
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




[Swift example]

1. download sunbighttp.xcframework.zip 
	- unzip and copy to project folder.
	- add to project.

2. info.plist

	- Add 'App Transport Security Settings'.

	- ex)
~~~
		<key>NSAppTransportSecurity</key>
		<dict>
			<key>NSAllowsArbitraryLoads</key>
			<true/>
		</dict>	
~~~

3. Usage


	3.1. header import

		import sunbighttp



	3.2. GET request

	    @IBAction func btn_get(_ sender: Any)
	    {
	        let sURL = "http://yourdomain-port/json/?page=2&city=XXXXX"
	        let sContentType = "application/x-www-form-urlencoded"
	        var dicParam = [
	            "nickname": "test10"
	        ]
	        let gtk = SBHttp()
	        gtk.get(sURL, withParam: dicParam) { error, data in
	            if error != nil {
	                print("error: %@", error.localizedDescription)
	                return
	            }
	            if(data != nil) {

	                do {
	                    let sJson = try JSONSerialization.jsonObject(with: data, options: .mutableContainers)
	                    print(sJson)
	                } catch let jsonError {
	                    print(jsonError)
	                }
	            }
	        }
	        
	    }


	3.3. POST (x-www-form-urlencoded)		



	    @IBAction func btn_post_encoded(_ sender: Any)
	    {
	        let sURL = "http://yourdomain-port/json/add1"
	        let sContentType = "application/x-www-form-urlencoded"
	        var dicParam = [
	            "nickname": "test10"
	        ]
	        let gtk = SBHttp()
	        gtk.post(sURL, withParam: dicParam, withAttach: [], contentType: sContentType) {
	        	 error, data in
	        	 
	            if error != nil {
	                print("error: %@", error.localizedDescription)
	                return
	            }
	            if(data != nil) {

	                do {
	                    let sJson = try JSONSerialization.jsonObject(with: data, options: .mutableContainers)
	                    print(sJson)
	                } catch let jsonError {
	                    print(jsonError)
	                }
	            }
	        }
	        
	    }

	3.4. POST (JSON)		

	    @IBAction func btn_post_json(_ sender: Any)
	    {
	        let sURL = "http://yourdomain-port/json/add1"
	        let sContentType = "application/json"
	        var dicParam = [
	            "nickname": "test10"
	        ]
	        let gtk = SBHttp()
	        
	        gtk.post(sURL, withParam: dicParam, withAttach: [], contentType: sContentType) { error, data in
	            if error != nil {
	                print("error: %@", error.localizedDescription)
	                return
	            }
	            if(data != nil) {

	                do {
	                    let sJson = try JSONSerialization.jsonObject(with: data, options: .mutableContainers)
	                    print(sJson)
	                } catch let jsonError {
	                    print(jsonError)
	                }
	            }
	        }
	    }

	3.5. POST (Files)

	     - HTML 
	     <input type="file" name="file1">
	     <input type="file" name="file2">

	    @IBAction func btn_post_files(_ sender: Any)
	    {
	        let sURL = "http://yourdomain-port/json/add2"
	        let sContentType = "application/json"
	        var dicParam = [
	            "nickname": "test10"
	        ]
	        var arrAttachFiles = [
	            UIImage(named: "koala"), UIImage(named: "koala-2")
	        ]
	        var arrAttachNames = [
	            "koala.png", "koala-2.png"
	        ]
	        var arrAttachData = [[String:Any]]()
	        for (index, img) in arrAttachFiles.enumerated() {
	            
	            let d1 = arrAttachFiles[index]!.jpegData(compressionQuality: 1.0)
	            let f1 = arrAttachNames[index]
 		    let k1 = "file\(index+1)"
	            
	            let dic:[String:Any] = ["Data": d1, "Filename": f1, "Name": k1]
	            arrAttachData.append(dic)
	        }
	        
	        
	        let gtk = SBHttp()
	        
	        gtk.post(sURL, withParam: dicParam, withAttach: arrAttachData, contentType: sContentType) { error, data in
	            if error != nil {
	                print("error: %@", error.localizedDescription)
	                return
	            }
	            if(data != nil) {

	                do {
	                    let sJson = try JSONSerialization.jsonObject(with: data, options: .mutableContainers)
	                    print(sJson)
	                } catch let jsonError {
	                    print(jsonError)
	                }
	            }
	        }
	    }
	    
	    
	    
	    
[Copyright]  
This SunBigHttp library is free for personal use only. 
For other uses, a legal license is required; contact tomtomsoft@naver.com.


