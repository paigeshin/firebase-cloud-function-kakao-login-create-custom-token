# firebase-cloud-function-kakao-login-create-custom-token

```swift
exports.createCustomTokenWithKakao = functions.https.onCall(
  async (data, context) => {
    const uid = `kakao:${data.uid}`;
    const updateParams = {
      email: user.email,
      displayName: user.displayName,
    };
    try {
      await admin.auth().updateUser(uid, updateParams);
    } catch (error) {
      updateParams["uid"] = uid;
      await admin.auth().createUser(updateParams);
    }
    const token = await admin.auth().createCustomToken(uid);
    return {
      token: token,
    };
  }
);

```
