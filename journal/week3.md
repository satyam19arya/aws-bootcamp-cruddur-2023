# Week 3 — Decentralized Authentication

Using the AWS Console we'll create a Cognito User Group

<img width="665" alt="image" src="https://user-images.githubusercontent.com/77580311/226923576-45ba53dc-4c17-4903-a745-82ce926166b2.png">

# Amplify
Install AWS Amplify
```
cd frontend-react-js/
npm i aws-amplify --save
```

We need to hook up our cognito pool to our code in the App.js
```
import { Amplify } from 'aws-amplify';

Amplify.configure({
  "AWS_PROJECT_REGION": process.env.REACT_APP_AWS_PROJECT_REGION,
  "aws_cognito_region": process.env.REACT_APP_AWS_COGNITO_REGION,
  "aws_user_pools_id": process.env.REACT_APP_AWS_USER_POOLS_ID,
  "aws_user_pools_web_client_id": process.env.REACT_APP_CLIENT_ID,
  "oauth": {},
  Auth: {
    // We are not using an Identity Pool
    // identityPoolId: process.env.REACT_APP_IDENTITY_POOL_ID, // REQUIRED - Amazon Cognito Identity Pool ID
    region: process.env.REACT_APP_AWS_PROJECT_REGION,           // REQUIRED - Amazon Cognito Region
    userPoolId: process.env.REACT_APP_AWS_USER_POOLS_ID,         // OPTIONAL - Amazon Cognito User Pool ID
    userPoolWebClientId: process.env.REACT_APP_CLIENT_ID,   // OPTIONAL - Amazon Cognito Web Client ID (26-char alphanumeric string)
  }
});
```

Copy the following code in docker-compose.yml in frontend part
```
      REACT_APP_AWS_PROJECT_REGION: "${AWS_DEFAULT_REGION}"
      REACT_APP_AWS_COGNITO_REGION: "${AWS_DEFAULT_REGION}"
      REACT_APP_AWS_USER_POOLS_ID: ""
      REACT_APP_CLIENT_ID: ""
```

# Conditionally show components based on logged in or logged out
Inside HomeFeedPage.js
```
import { Auth } from 'aws-amplify';

// set a state
const [user, setUser] = React.useState(null);

const checkAuth = async () => {
    Auth.currentAuthenticatedUser({
      // Optional, By default is false. 
      // If set to true, this call will send a 
      // request to Cognito to get the latest user data
      bypassCache: false 
    })
    .then((user) => {
      console.log('user',user);
      return Auth.currentAuthenticatedUser()
    }).then((cognito_user) => {
        setUser({
          display_name: cognito_user.attributes.name,
          handle: cognito_user.attributes.preferred_username
        })
    })
    .catch((err) => console.log(err));
  };


// check when the page loads if we are authenticated
React.useEffect(()=>{
  loadData();
  checkAuth();
}, [])
```
We'll want to pass user to the following components:
```
<DesktopNavigation user={user} active={'home'} setPopped={setPopped} />
<DesktopSidebar user={user} />
```

We'll check DesktopNavigation.js so that it it conditionally shows links in the left hand column on whether you are logged in or not.
Notice we are passing the user to ProfileInfo
```
import './DesktopNavigation.css';
import {ReactComponent as Logo} from './svg/logo.svg';
import DesktopNavigationLink from '../components/DesktopNavigationLink';
import CrudButton from '../components/CrudButton';
import ProfileInfo from '../components/ProfileInfo';

export default function DesktopNavigation(props) {

  let button;
  let profile;
  let notificationsLink;
  let messagesLink;
  let profileLink;
  if (props.user) {
    button = <CrudButton setPopped={props.setPopped} />;
    profile = <ProfileInfo user={props.user} />;
    notificationsLink = <DesktopNavigationLink 
      url="/notifications" 
      name="Notifications" 
      handle="notifications" 
      active={props.active} />;
    messagesLink = <DesktopNavigationLink 
      url="/messages"
      name="Messages"
      handle="messages" 
      active={props.active} />
    profileLink = <DesktopNavigationLink 
      url="/@andrewbrown" 
      name="Profile"
      handle="profile"
      active={props.active} />
  }

  return (
    <nav>
      <Logo className='logo' />
      <DesktopNavigationLink url="/" 
        name="Home"
        handle="home"
        active={props.active} />
      {notificationsLink}
      {messagesLink}
      {profileLink}
      <DesktopNavigationLink url="/#" 
        name="More" 
        handle="more"
        active={props.active} />
      {button}
      {profile}
    </nav>
  );
}
```

We'll update ProfileInfo.js
```
import { Auth } from 'aws-amplify';

const signOut = async () => {
  try {
      await Auth.signOut({ global: true });
      window.location.href = "/"
  } catch (error) {
      console.log('error signing out: ', error);
  }
}
```
We'll check DesktopSidebar.js so that it conditionally shows components in case you are logged in or not.
# Signin Page
```
import { Auth } from 'aws-amplify';

 const onsubmit = async (event) => {
    setErrors('')
    event.preventDefault();
    Auth.signIn(email, password)
    .then(user => {
      console.log('user',user)
      localStorage.setItem("access_token", user.signInUserSession.accessToken.jwtToken)
      window.location.href = "/"
    })
    .catch(error => { 
      if (error.code == 'UserNotConfirmedException') {
        window.location.href = "/confirm"
      }
      setErrors(error.message)
    });
    return false
  }
```

Create a user in Cognito and to confirm the user, run the command:
```
aws cognito-idp admin-set-user-password --username satyam19arya --password Testing1234! --user-pool-id us-east-1_caIgbml5U --permanent
```
Then sign-in to your account using username and password:
<img width="499" alt="image" src="https://user-images.githubusercontent.com/77580311/229343392-768c522b-1c50-4120-bfcd-6fe4d0562ea7.png">

Sign-in successfull
<img width="941" alt="image" src="https://user-images.githubusercontent.com/77580311/229343441-1a0b13a7-2e00-45a6-b4ea-82f968ef7a56.png">

Now we edit user attributes and upload name and preferred_username
<img width="658" alt="image" src="https://user-images.githubusercontent.com/77580311/229343872-e0ca1cda-d426-4311-ba69-8b8114ec2025.png">

<img width="486" alt="image" src="https://user-images.githubusercontent.com/77580311/229343962-3e77b55c-c77d-4602-ac81-86db6326d005.png">

Again sign-in to your account using username and password:
<img width="212" alt="image" src="https://user-images.githubusercontent.com/77580311/229344031-7ecdac63-164b-4e9a-afce-d0812a27e781.png">

Now delete the user and let's create a sign-up page




