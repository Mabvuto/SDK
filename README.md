pod “PinterestSDK”, :git => “git@github.com:pinterest/ios-pdk.git”
<key>CFBundleURLTypes</key>
  <array>
    <dict>
      <key>CFBundleURLName</key>
      <string></string>
      <key>CFBundleURLSchemes</key>
      <array>
        <string>pdk{your-app-id}</string>
      </array>
    </dict>
  </array>
  [[PDKClient sharedInstance] authenticateWithPermissions:@[PDKClientReadPublicPermissions,
                                                          PDKClientWritePublicPermissions,
                                                          PDKClientReadPrivatePermissions,
                                                          PDKClientWritePrivatePermissions,
                                                          PDKClientReadRelationshipsPermissions,
                                                          PDKClientWriteRelationshipsPermissions]
                                            withSuccess:^(PDKResponseObject *responseObject)
{
    PDKUser *user = [responseObject user];
    NSLog(@"%@ authenticated!", user.firstName);
} andFailure:^(NSError *error) {
    NSLog(@"authentication failed: %@", error);
}];
- (BOOL)application:(UIApplication *)application handleOpenURL:(NSURL *)url
{
    return [[PDKClient sharedInstance] handleCallbackURL:url];
}
Making requests
/** @param path         The path to endpoint
 *  @param parameters   Any parameters that need to be sent to the endpoint
 *  @param successBlock Called when the API call succeeds
 *  @param failureBlock Called when the API call fails
 */
- (void)getPath:(NSString *)path
     parameters:(NSDictionary *)parameters
    withSuccess:(PDKClientSuccess)successBlock
     andFailure:(PDKClientFailure)failureBlock;
/** @param path         The path to the endpoint
 *  @param parameters   Any parameters that need to be sent to the endpoint
 *  @param successBlock Called when the API call succeeds
 *  @param failureBlock Called when the API call fails
 */
- (void)deletePath:(NSString *)path
        parameters:(NSDictionary *)parameters
       withSuccess:(PDKClientSuccess)successBlock
        andFailure:(PDKClientFailure)failureBlock;
