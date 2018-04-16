# recetteApp-exercices-instructions

To install angular-cli globally, type the following at the prompt:

```javascript
npm install -g @angular/cli
```

## Generating and Serving an Angular Project using Angular-CLI

```javascript
ng new recetteApp -dir=<The path of your Angular folder>/recetteApp --style=scss
```

Move to the recetteApp folder and type the following at the prompt:

```javascript
npm install
ng serve --open
```
### Adding a Menu Component

First, download the images.zip file provided above and then unzip the file. Move the resulting images folder containing some PNG files to the Angular project's src/assets folder.

```javascript
ng generate component menu
```
Next, open app.component.html file and add the following after the toolbar:

```javascript
<app-menu></app-menu>
```
### Creating the Menu

Next, create a folder named shared under the src/app/shared folder. To this folder, add a file named plat.ts with the following code:
```javascript
export class Plat {
    name: string;
    image: string;
    category: string;
    label: string;
    price: string;
    description: string;
}
```
Update menu.component.ts as follows to add in the data for four menu items:
```javascript
. . .
import { Plat } from '../shared/plat';
. . .

export class MenuComponent implements OnInit {

  plats: Plat[] = [
                         {
                           name:'Uthappizza',
                           image: '/assets/images/uthappizza.png',
                           category: 'mains',
                           label:'Hot',
                           price:'4.99',
                           description:'A unique combination of Indian Uthappam (pancake) and Italian pizza, topped with Cerignola olives, ripe vine cherry tomatoes, Vidalia onion, Guntur chillies and Buffalo Paneer.'                        },
                        {
                           name:'Zucchipakoda',
                           image: '/assets/images/zucchipakoda.png',
                           category: 'appetizer',
                           label:'',
                           price:'1.99',
                           description:'Deep fried Zucchini coated with mildly spiced Chickpea flour batter accompanied with a sweet-tangy tamarind sauce'                        },
                        {
                           name:'Vadonut',
                           image: '/assets/images/vadonut.png',
                           category: 'appetizer',
                           label:'New',
                           price:'1.99',
                           description:'A quintessential ConFusion experience, is it a vada or is it a donut?'                        },
                        {
                           name:'ElaiCheese Cake',
                           image: '/assets/images/elaicheesecake.png',
                           category: 'dessert',
                           label:'',
                           price:'2.99',
                           description:'A delectable, semi-sweet New York Style Cheese Cake, with Graham cracker crust and spiced with Indian cardamoms'                        }
                        ];
. . .
}
```
To configure your project to use Angular material, type the following at the prompt to install Angular Material, Angular Animations and HammerJS:
```javascript
npm install --save @angular/material @angular/cdk
npm install --save @angular/animations
npm install --save hammerjs
npm install --save @angular/flex-layout@latest
```
Configure to use Material Design Icons
Next, include the following into the <head> of index.html to make use of Material Design icons:
  
```javascript
<link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet"> 
```
Updating AppModule
Then, you need to import the Angular Animations Module, Angular Material Module, Flex Layout Module and hammerjs into your root module (src/app/app.module.ts) as follows:
```javascript
. . . 
import { BrowserAnimationsModule } from '@angular/platform-browser/animations';
import { FlexLayoutModule }  from '@angular/flex-layout';
import { MatListModule, MatInputModule } from '@angular/material';
import { MatGridListModule } from '@angular/material';
import { MatCardModule } from '@angular/material/card';
import { MatButtonModule } from '@angular/material';
import { MatToolbarModule } from '@angular/material';
import { MatDialogModule } from '@angular/material';
import { MatCheckboxModule } from '@angular/material';

. . . 

import 'hammerjs';

@NgModule({
  
  . . . 
  
  imports: [ 
    
    . . .,
    MatGridListModule,
    FlexLayoutModule,
    MatListModule,
    MatCardModule,
    MatButtonModule,
    MatToolbarModule,
    MatInputModule,
    BrowserAnimationsModule;
    MatDialogModule,
    MatCheckboxModule,
    
  ], 
    
    . . . 
  
  
}) 

. . . 
```
Open app.component.html and replace its contents with the following code:
```javascript
<mat-toolbar color="primary"> <span>Restaurant des Recettes</span> </mat-toolbar>
```
Next, update the menu.component.html template as follows:

```javascript
<div class="container"
     fxLayout="column"
     fxLayoutGap="10px">

<mat-list fxFlex>
  <mat-list-item *ngFor="let plat of plats">
    <img mat-list-avatar src={{plat.image}} alt={{plat.name}}>
    <h1 mat-line> {{plat.name}} </h1>
    <p mat-line>
      <span> {{plat.description}} </span>
    </p>
  </mat-list-item>
</mat-list>
```
Add the following CSS class to styles.scss file:
```javascript
@import '~@angular/material/prebuilt-themes/deeppurple-amber.css';
.container {
    margin: 20px;
    display:flex;
}

body { 
  padding: 0; 
  margin: 0; 
  font-family: Roboto, sans-serif; 
  
}

```
Updating the Menu Template

Open menu.component.html and update its content as follows:
```javascript
<<div class="container"
     fxLayout="column"
     fxLayoutGap="10px">

  <div fxFlex>
    <div>
      <h3>Menu</h3>
      <hr>
    </div>
  </div>

  <div fxFlex>
    <mat-grid-list cols="2" rowHeight="200px">
      <mat-grid-tile *ngFor="let plat of plats">
        <img height="200px" src={{plat.image}} alt={{plat.name}}>
        <mat-grid-tile-footer>
          <h1 mat-line>{{plat.name | uppercase}}</h1>
        </mat-grid-tile-footer>
      </mat-grid-tile>
    </mat-grid-list>
  </div>

  <div fxFlex *ngIf="selectedPlat">
    <mat-card>
      <mat-card-header>
        <mat-card-title>
          <h3>{{selectedPlat.name | uppercase}}</h3>
        </mat-card-title>
      </mat-card-header>
      <img mat-card-image src={{selectedPlat.image}} alt={{selectedPlat.name}}>
      <mat-card-content>
        <p>{{selectedPlat.description}}
        </p>
      </mat-card-content>
      <mat-card-actions>
        <button mat-button>LIKE</button>
        <button mat-button>SHARE</button>
      </mat-card-actions>
    </mat-card>
  </div>

</div>
```
Also, update the menu.component.ts file as follows to move the details of the plats into a constant
```javascript
 . . .
 
 const PLATS: Plat[] = [
 . . .
 
 ];
 
 . . .
 
 export class MenuComponent implements OnInit {

  plats = PLATS;

  selectedPlat = PLATS[0];

 . . .
 
 }
 ```
### Exercice Fin module

Task 1

In this task you will be adding a new platdetail component to your Angular application and include the component into the menu component's template so that the details of a specific plat are displayed there:

- Use Angular CLI to create a new component named platdetail,
- Replace the card showing the selected plat in menu component's template with the platdetail component, and
- Update the template of the platdetail component with the following code:

```javascript
<div class="container"
    fxLayout="row"
    fxLayout.sm="column"
    fxLayout.xs="column"
    fxLayoutAlign.gt-mat="space-around center"
    fxLayoutGap="10px" 
    fxLayoutGap.xs="0">

  <div fxFlex="40" *ngIf="plat" >
    <p>Afficher le detail ici</p>
 </div>

  <div fxFlex="20" *ngIf="plat">
      <p>Afficher les commentaires ici</p>
 </div>

</div>
 ```
 Task 2

In this task you will be adding a card component to the platdetail template to display the details of the plat given above:

Add a new constant to the platdetail.component.ts file named PLAT as follows, and initialize it to the JavaScript object given below that contains the details of the plat and comments about the plat:
```javascript
const PLAT = {
  name: 'Uthappizza',
  image: '/assets/images/uthappizza.png',
  category: 'mains',
  label: 'Hot',
  price: '4.99',
  description: 'A unique combination of Indian Uthappam (pancake) and Italian pizza, topped with Cerignola olives, ripe vine cherry tomatoes, Vidalia onion, Guntur chillies and Buffalo Paneer.',
  comments: [
    {
      rating: 5,
      comment: "Imagine all the eatables, living in conFusion!",
      author: "John Lemon",
      date: "2012-10-16T17:57:28.556094Z"
    },
    {
      rating: 4,
      comment: "Sends anyone to heaven, I wish I could get my mother-in-law to eat it!",
      author: "Paul McVites",
      date: "2014-09-05T17:57:28.556094Z"
    },
    {
      rating: 3,
      comment: "Eat it, just eat it!",
      author: "Michael Jaikishan",
      date: "2015-02-13T17:57:28.556094Z"
    },
    {
      rating: 4,
      comment: "Ultimate, Reaching for the stars!",
      author: "Ringo Starry",
      date: "2013-12-02T17:57:28.556094Z"
    },
    {
      rating: 2,
      comment: "It's your birthday, we're gonna party!",
      author: "25 Cent",
      date: "2011-12-02T17:57:28.556094Z"
    }
  ]
};
```
Now introduce a new variable in the platdetail.component.ts file in the platdetail class called plat
and set it equal to the PLAT constant above:
```javascript
plat = PLAT;
```
The Angular material card component should be used to display the details of the plat as shown above. Please remember to use the Angular "uppercase" pipe on the name displayed in the card title. Also apply the *ngIf="plat" structural directive to both the <mat-card>.

Task 3

In this task you will use the comments that are included in the plat object above to display a list of the comments.

This task involves the following steps:

Use the Angular material list to display the list of comments as shown below. Also apply the *ngIf="plat" structural directive to both the <md-list> that displays the list of comments .
Display the date of the comment by processing it through the Angular built-in date pipe.

### Data binding

Refactoring the Code :

First, create a new class named Comment in a file named comment.ts in the shared folder and include the following in it:

```javascript
export class Comment {
    rating: number;
    comment: string;
    author: string;
    date: string;
}
```
Then update the plat class to allow a plat to have an array of comments as follows:

```javascript
import { Comment } from './comment';

export class Plat {
    name: string;
    image: string;
    category: string;
    label: string;
    price: string;
    description: string;
    comments: Comment[];
}
```
Then create a new file named plats.ts in the shared folder to now export the JavaScript object array of plats:


```javascript
import { Plat } from './plat';

export const PLATS: Plat[] = [
    {
        name: 'Uthappizza',
        image: '/assets/images/uthappizza.png',
        category: 'mains',
        label: 'Hot',
        price: '4.99',
        description: 'A unique combination of Indian Uthappam (pancake) and Italian pizza, topped with Cerignola olives, ripe vine cherry tomatoes, Vidalia onion, Guntur chillies and Buffalo Paneer.',
        comments: [
            {
                rating: 5,
                comment: "Imagine all the eatables, living in conFusion!",
                author: "John Lemon",
                date: "2012-10-16T17:57:28.556094Z"
            },
            {
                rating: 4,
                comment: "Sends anyone to heaven, I wish I could get my mother-in-law to eat it!",
                author: "Paul McVites",
                date: "2014-09-05T17:57:28.556094Z"
            },
            {
                rating: 3,
                comment: "Eat it, just eat it!",
                author: "Michael Jaikishan",
                date: "2015-02-13T17:57:28.556094Z"
            },
            {
                rating: 4,
                comment: "Ultimate, Reaching for the stars!",
                author: "Ringo Starry",
                date: "2013-12-02T17:57:28.556094Z"
            },
            {
                rating: 2,
                comment: "It's your birthday, we're gonna party!",
                author: "25 Cent",
                date: "2011-12-02T17:57:28.556094Z"
            }
        ]
    },
    {
        name: 'Zucchipakoda',
        image: '/assets/images/zucchipakoda.png',
        category: 'appetizer',
        label: '',
        price: '1.99',
        description: 'Deep fried Zucchini coated with mildly spiced Chickpea flour batter accompanied with a sweet-tangy tamarind sauce',
        comments: [
            {
                rating: 5,
                comment: "Imagine all the eatables!",
                author: "John Lemon",
                date: "2012-10-16T17:57:28.556094Z"
            },
            {
                rating: 4,
                comment: "Sends anyone to heaven, I wish I could get my mother-in-law to eat it!",
                author: "Paul McVites",
                date: "2014-09-05T17:57:28.556094Z"
            },
            {
                rating: 3,
                comment: "Eat it, just eat it!",
                author: "Michael Jaikishan",
                date: "2015-02-13T17:57:28.556094Z"
            },
            {
                rating: 4,
                comment: "Ultimate, Reaching for the stars!",
                author: "Ringo Starry",
                date: "2013-12-02T17:57:28.556094Z"
            },
            {
                rating: 2,
                comment: "It's your birthday, we're gonna party!",
                author: "25 Cent",
                date: "2011-12-02T17:57:28.556094Z"
            }
        ]
    },
    {
        name: 'Vadonut',
        image: '/assets/images/vadonut.png',
        category: 'appetizer',
        label: 'New',
        price: '1.99',
        description: 'A quintessential ConFusion experience, is it a vada or is it a donut?',
        comments: [
            {
                rating: 5,
                comment: "Imagine all the eatables, living in conFusion!",
                author: "John Lemon",
                date: "2012-10-16T17:57:28.556094Z"
            },
            {
                rating: 4,
                comment: "Sends anyone to heaven, I wish I could get my mother-in-law to eat it!",
                author: "Paul McVites",
                date: "2014-09-05T17:57:28.556094Z"
            },
            {
                rating: 3,
                comment: "Eat it, just eat it!",
                author: "Michael Jaikishan",
                date: "2015-02-13T17:57:28.556094Z"
            },
            {
                rating: 4,
                comment: "Ultimate, Reaching for the stars!",
                author: "Ringo Starry",
                date: "2013-12-02T17:57:28.556094Z"
            },
            {
                rating: 2,
                comment: "It's your birthday, we're gonna party!",
                author: "25 Cent",
                date: "2011-12-02T17:57:28.556094Z"
            }
        ]
    },
    {
        name: 'ElaiCheese Cake',
        image: '/assets/images/elaicheesecake.png',
        category: 'dessert',
        label: '',
        price: '2.99',
        description: 'A delectable, semi-sweet New York Style Cheese Cake, with Graham cracker crust and spiced with Indian cardamoms',
        comments: [
            {
                rating: 5,
                comment: "Imagine all the eatables, living in conFusion!",
                author: "John Lemon",
                date: "2012-10-16T17:57:28.556094Z"
            },
            {
                rating: 4,
                comment: "Sends anyone to heaven, I wish I could get my mother-in-law to eat it!",
                author: "Paul McVites",
                date: "2014-09-05T17:57:28.556094Z"
            },
            {
                rating: 3,
                comment: "Eat it, just eat it!",
                author: "Michael Jaikishan",
                date: "2015-02-13T17:57:28.556094Z"
            },
            {
                rating: 4,
                comment: "Ultimate, Reaching for the stars!",
                author: "Ringo Starry",
                date: "2013-12-02T17:57:28.556094Z"
            },
            {
                rating: 2,
                comment: "It's your birthday, we're gonna party!",
                author: "25 Cent",
                date: "2011-12-02T17:57:28.556094Z"
            }
        ]
    }
];
```
Updating the Menu Component:

Open menu.component.ts file and update its content, first by deleting the plats constant and then make the following changes:

```javascript
import { Component, OnInit } from '@angular/core';
import { Plat } from '../shared/plat';
import { PLATS } from '../shared/plats';

. . .

export class MenuComponent implements OnInit {

  plats = PLATS;

  selectedPlat: Plat;

. . .

  onSelect(plat: Plat) {
    this.selectedPlat = plat;
  }

}
```
Then update the menu.component.html file as follows:

```javascript
. . .

      <md-grid-tile *ngFor="let plat of plats" (click) = "onSelect(plat)">
        . . .
        
  <app-detail-plat [plat] = "selectedPlat"></app-detail-plat>
        
. . .
```
Open detail-plat.component.ts and update its contents as follows :
```javascript
import { Component, OnInit, Input } from '@angular/core';
import { Plat } from '../shared/plat';

. . .

export class DetailPlatComponent implements OnInit {

  @Input()
  plat: Plat;

. . .
```
Adding a Service 

Create a folder named services in the src/app folder.
```javascript
ng generate service services/plat
```
Open plat.service.ts and update its contents and add the service to the app.module.ts:
```javascript
import { Injectable } from '@angular/core';
import { Plat } from '../shared/plat';
import { PLATS } from '../shared/plats';

@Injectable()
export class PlatService {

  constructor() { }

  getPlats(): Plat[] {
    return PLATS;
  }
}
```
Using the Service
Now update menu.component.ts file to make use of the service as follows:

```javascript
constructor(private platService: PlatService) { }
  
  ngOnInit() {
    this.plats = this.platService.getPlats();
  }
```
### Header and Footer

First use NPM to fetch Font Awesome to the project by typing the following at the prompt:
```javascript
npm install font-awesome --save
```
Then, open the .angular-cli.json file in the project's root folder and update it as follows:
```javascript
"styles": [
        "styles.scss",
        "../node_modules/font-awesome/scss/font-awesome.scss"
      ],
```
Create two new components named header and footer.

Update the footer's template as follows:
```javascript
<div class="container footer" 
    fxLayout="row" 
    fxLayout.sm="column" 
    fxLayout.xs="column" 
    fxLayoutAlign.xs="start center" 
    fxLayoutAlign.sm="start center"
    fxLayoutAlign.gt-sm="center center" 
    fxLayoutWrap 
    fxLayoutGap="10px">

  <div fxFlex="100%" fxFlex.gt-sm="50%">
    <div fxLayout="row">
      <div fxFlex="40" fxFlexOffset="20px">
        <h4>Links</h4>
        <mat-list>
          <mat-list-item><a mat-button>Home</a></mat-list-item>
          <mat-list-item><a mat-button>About</a></mat-list-item>
          <mat-list-item><a mat-button>Menu</a></mat-list-item>
          <mat-list-item><a mat-button>Contact</a></mat-list-item>
        </mat-list>
      </div>
      <div fxFlex="50">
        <h4>Our Address</h4>
        <address style="text-size: 80%">
          121, Clear Water Bay Road<br> Clear Water Bay, Kowloon<br> Rabat<br>
          <i class="fa fa-phone"></i>: +852 1234 5678<br>
          <i class="fa fa-fax"></i>: +852 8765 4321<br>
          <i class="fa fa-envelope"></i>:
          <a href="mailto:recetteApp@food.net">recetteApp@food.net</a>
        </address>
      </div>
    </div>
  </div>
  <div fxFlex="100%" fxFlex.gt-sm="45%">
    <div style="text-align:center">
      <a mat-icon-button class="btn-google-plus" href="http://google.com/+"><i class="fa fa-google-plus fa-lg"></i></a>
      <a mat-icon-button class="btn-facebook" href="http://www.facebook.com/profile.php?id="><i class="fa fa-facebook fa-lg"></i></a>
      <a mat-icon-button class="btn-linkedin" href="http://www.linkedin.com/in/"><i class="fa fa-linkedin fa-lg"></i></a>
      <a mat-icon-button class="btn-twitter" href="http://twitter.com/"><i class="fa fa-twitter fa-lg"></i></a>
      <a mat-icon-button class="btn-youtube" href="http://youtube.com/"><i class="fa fa-youtube fa-lg"></i></a>
      <a mat-icon-button class="btn-mail" href="mailto:"><i class="fa fa-envelope-o fa-lg"></i></a>
    </div>
  </div>
  <div fxFlex="100" fxFlexAlign="center center">
    <div style="text-align:center;">
      <p>© Copyright 2017 Restaurant RecetteApp</p>
    </div>
  </div>
</div>
```
Update the footer's styles file as follows:
```javascript
$lt-gray: #ddd;
$background-dark: #512DA8;
$background-light: #9575CD;
$background-pale: #D1C4E9;

@mixin zero-margin($pad-up-down, $pad-left-right) {
    margin: 0px auto;
    padding: $pad-up-down $pad-left-right;
}

.footer{
    background-color: $background-pale;
    @include zero-margin(20px, 0px);
}

.btn-facebook {color:#fff!important; background-color:#3b5998!important;}
.btn-google-plus{color:#fff!important;background-color:#dd4b39!important;}
.btn-youtube{color:#fff!important;background-color:#ff4b39!important;}
.btn-linkedin{color:#fff!important;background-color:#007bb6!important;}
.btn-twitter{color:#fff!important;background-color:#55acee!important;}
.btn-mail{color:#fff!important;background-color:#512DA8!important;}
```
Update the header's template as follows:
```javascript
<mat-toolbar color="primary">
    <span><img src="/assets/images/logo.png" height=30 width=41></span>
    <a mat-button><span class="fa fa-home fa-lg"></span> Home</a>
    <a mat-button><span class="fa fa-info fa-lg"></span> About</a>
    <a mat-button><span class="fa fa-list fa-lg"></span> Menu</a>
    <a mat-button><span class="fa fa-address-card fa-lg"></span> Contact</a>
  
  </mat-toolbar>
  
  <div class="container jumbotron"
      fxLayout="row"
      fxLayout.sm="column" 
      fxLayout.xs="column" 
      fxLayoutAlign.xs="start center"
      fxLayoutAlign.sm="start center" 
      fxLayoutAlign.gt-sm="center center" 
      fxLayoutGap="10px">
  
    <div fxFlex fxFlex.gt-sm="50%">
      <h1>Restaurant recette App</h1>
      <p>We take inspiration from the World best cuisines, and create a unique fusion experience</p>
    </div>
    <div fxFlex fxFlex.gt-sm="20%">
      <img src="/assets/images/logo.png" alt="Logo">
    </div>
    <div fxFlex></div>
  </div>

```
Update the header's style file as follows:
```javascript
$lt-gray: #ddd;
$background-dark: #512DA8;
$background-light: #9575CD;
$background-pale: #D1C4E9;

@mixin zero-margin($pad-up-down, $pad-left-right) {
    margin: 0px auto;
    padding: $pad-up-down $pad-left-right;
}

.jumbotron {
    @include zero-margin(70px,30px);
    background: $background-light ;
    color:floralwhite;
    min-height: 150px;
}
```
Update the project's style file styles.scss with the following:
```javascript
. . .


$lt-gray: #ddd;
$background-dark: #512DA8;
$background-light: #9575CD;
$background-pale: #D1C4E9;
$primary-color-dark:   #512DA8;
$primary-color:        #673AB7;
$primary-color-light:  #D1C4E9;
$primary-color-text:   #FFFFFF;
$accent-color:         #FFC107;
$primary-text-color:   #212121;
$secondary-text-color: #757575;
$divider-color:        #BDBDBD;

@mixin zero-margin($pad-up-down, $pad-left-right) {
    margin: 0px auto;
    padding: $pad-up-down $pad-left-right;
}

. . .


.background-primary {
    background-color: $background-dark!important;
  }
.background-accent {
    background-color: $accent-color!important;
  }
.text-floral-white {
    color: floralwhite!important;
}

.flex-spacer {
  flex: 1 1 auto;
}
```
Now update the app.component.html file to include the header and footer as follows:
```javascript
<app-header></app-header>
<app-menu></app-menu>
<app-footer></app-footer>
```
### Angular Routing

Add three new components to your Angular :about,home,contact.

Add a new module named app-routing to your application as follows. This will create a new module file named app-routing.module.ts in the app-routing folder.

```javascript
ng generate module app-routing
```
Next create a new file named routes.ts in the app-routing folder and update it as follows:
```javascript
import { Routes } from '@angular/router';

import { MenuComponent } from '../menu/menu.component';
import { DetailPlatComponent } from '../detail-plat/detail-plat.component';
import { HomeComponent } from '../home/home.component';
import { AboutComponent } from '../about/about.component';
import { ContactComponent } from '../contact/contact.component';

export const routes: Routes = [
  { path: 'home',  component: HomeComponent },
  { path: 'menu',     component: MenuComponent },
  { path: '', redirectTo: '/home', pathMatch: 'full' }
];
```
Update the app-routing.module.ts file to make use of the routes defined above as follows and don't forget to add it to app.module.ts.

```javascript
import { NgModule } from '@angular/core';
import { CommonModule } from '@angular/common';
import { RouterModule, Routes } from '@angular/router';

import { routes } from './routes';

@NgModule({
  imports: [
    CommonModule,
    RouterModule.forRoot(routes)
  ],
  exports: [ RouterModule ],
  declarations: []
})
export class AppRoutingModule { }
```
Next update the app.component.html file :
```javascript
<app-header></app-header>
<router-outlet></router-outlet>
<app-footer></app-footer>
```
Finally update the toolbar in the header.component.html file as follows:
```javascript
<mat-toolbar color="primary">
        <span><img src="/assets/images/logo.png" height=30 width=41></span>
        <a mat-button routerLink="/home"><span class="fa fa-home fa-lg"></span> Home</a>
        <a mat-button><span class="fa fa-info fa-lg"></span> About</a>
        <a mat-button routerLink="/menu"><span class="fa fa-list fa-lg"></span> Menu</a>
        <a mat-button><span class="fa fa-address-card fa-lg"></span> Contact</a>
      
</mat-toolbar>
```
Update each of the links in the toolbar with the following addition to the link:

```javascript
<a . . . routerLinkActive="active"><span . . . ></span> Home</a>
```
Now add the following scss class to header.component.scss:
```javascript
$background-moredark: #4527A0;
. . .
.active {
    background: $background-moredark;
}
```
update plat.ts file
```javascript
import { Comment } from './comment';

export class Plat {
    id: number;
    name: string;
    image: string;
    category: string;
    label: string;
    price: string;
    featured: boolean;
    description: string;
    comments: Comment[];
}
```
Now that we added the id and featured property to plat, update the PLATS constant in plats.ts

Now update the plat service to return a specific plat, and a featured plat as follows:
```javascript
getPlat(id: number): Plat {
    return PLATS.filter((plat) => (plat.id === id))[0];
  }

  getFeaturedPlat(): Plat {
    return PLATS.filter((plat) => plat.featured)[0];
  }
```
Next add promotion.ts file to the shared folder

```javascript
export class Promotion {
    id: number;
    name: string;
    image: string;
    label: string;
    price: string;
    featured: boolean;
    description: string;
}
```
Then, add promotions.ts file to the shared folder and update its contents as follows:

```javascript
import { Promotion } from './promotion';

export const PROMOTIONS: Promotion[] = [
    {
      id: 0,
      name: 'Weekend Grand Buffet',
      image: '/assets/images/buffet.png',
      label: 'New',
      price: '19.99',
      featured: true,
      description: 'Featuring mouthwatering combinations with a choice of five different salads, six enticing appetizers, six main entrees and five choicest desserts. Free flowing bubbly and soft drinks. All for just $19.99 per person'
    }
  ];
```
 Add a new service named "promotion" to the services folder with :
 ```javascript
 getPromotions(): Promotion[] {
    return PROMOTIONS;
  }

  getPromotion(id: number): Promotion {
    return PROMOTIONS.filter((promo) => (promo.id === id))[0];
  }

  getFeaturedPromotion(): Promotion {
    return PROMOTIONS.filter((promotion) => promotion.featured)[0];
  }
 ```
 update the home.component.ts file to fetch and provide the featured plat and promotion for the view:
 ```javascript
 promotion: Promotion;

  constructor(private platsService: PlatService,
    private promotionservice: PromotionService) { }

  ngOnInit() {
    this.plat = this.platService.getFeaturedPlat();
    this.promotion = this.promotionservice.getFeaturedPromotion();
  }
  ``` 
Open the routes.ts and add the following route to it:
```javascript
{ path: 'detailPlat/:id',     component: DetailPlatComponent }
 ``` 
 Open menu.component.html and update it as follows. Also remove the <app-detail-plat> from the template.
 ```javascript
 <mat-grid-tile *ngFor="let plat of plats" [routerLink]="['/detailPlat', plat.id]">
 ``` 
 Open detail-plat.component.ts and update it as follows:
  ```javascript
  plat: Plat;

  constructor(private platService: PlatService,
    private route: ActivatedRoute,
    private location: Location) { }

  ngOnInit() {
    let id = +this.route.snapshot.params['id'];
    this.plat = this.platService.getPlat(id);
  }

  goBack(): void {
    this.location.back();
  }
 ``` 
 open detail-plat.component.html and update it :
 ```javascript
  <mat-card-actions>
        <button mat-button>LIKE</button>
        <button mat-button>SHARE</button>
        <button md-button (click)="goBack()">BACK</button>
  </mat-card-actions>
 ```
Angular Forms :

Add a link to the toolbar in the header component, which when clicked will open a Login form in a dialog view:

```javascript
<a mat-button (click)="openLoginForm()"><span class="fa fa-sign-in fa-lg"></span> Login</a>
```
create an Angular component named LoginComponent

Add the FormsModule and the LoginComponent as follows:

```javascript
entryComponents: [
        LoginComponent
  ],
  imports: [ 
    . . . 
    
    FormsModule 
  ],
```
open header.component.ts and update it as follows:
```javascript
import { MatDialog, MatDialogRef } from '@angular/material';
import { LoginComponent } from '../login/login.component';

constructor(public dialog: MatDialog ) { }

  ngOnInit() {
  }

  openLoginForm() {
    this.dialog.open(LoginComponent, {width: '500px', height: '450px'});
  }

```
Open login.component.html file and add in the form as follows:
```javascript
<p>{{ user | json }}</p>

<form novalidate (ngSubmit)="onSubmit()">

  <mat-dialog-content>
    <p>
      <mat-input-container>
        <input matInput placeholder="Username" type="text" [(ngModel)]="user.username" name="username" required>
      </mat-input-container>
      <mat-input-container>
        <input matInput placeholder="Password" type="password" [(ngModel)]="user.password" name="password" required>
      </mat-input-container>
      <mat-checkbox [(ngModel)]="user.remember" name="remember">Remember Me</mat-checkbox>
    </p>
  </mat-dialog-content>
  <mat-dialog-actions>
    <span class="flex-spacer"></span>
    <button mat-button mat-dialog-close>Cancel</button>
    <button type="submit" mat-button class="background-primary text-floral-white" >Login</button>
  </mat-dialog-actions>
</form>
```
Then, open login.component.ts file and update its contents as follows:
```javascript
 user = {remember: false};

  constructor(public dialogRef: MatDialogRef<LoginComponent>) { }

  ngOnInit() {
  }

  onSubmit() {
    console.log("User: ", this.user);
    this.dialogRef.close();
  }
```
Open login.component.html file aand update its contents as follows:
```javascript
<p>{{ user | json }}</p>

<form novalidate #loginForm="ngForm" (ngSubmit)="onSubmit()">

  <mat-dialog-content>
    <p>
      <mat-input-container  dividerColor="{{username.invalid && !username.pristine ? 'warn' : 'primary'}}">
        <input matInput placeholder="Username" type="text" [(ngModel)]="user.username" name="username" #username="ngModel" required>
        <mat-hint>
            <span [hidden]="username.pristine">
            <span [hidden]="!username.errors?.required">username is required</span>
            </span>
          </mat-hint>
      </mat-input-container>
      <mat-input-container>
        <input matInput placeholder="Password" type="password" [(ngModel)]="user.password" name="password" #password="ngModel" required>
      </mat-input-container>
      <mat-checkbox [(ngModel)]="user.remember" name="remember">Remember Me</mat-checkbox>
    </p>
  </mat-dialog-content>
  <mat-dialog-actions>
    <span class="flex-spacer"></span>
    <button mat-button mat-dialog-close>Cancel</button>
    <button type="submit" mat-button class="background-primary text-floral-white"  [disabled]="loginForm.form.invalid">Login</button>
  </mat-dialog-actions>
</form>
```
update the services to operate using observables :

```javascript
import { Injectable } from '@angular/core';
import { Plat } from '../shared/plat';
import { PLATS } from '../shared/plats';
import { Observable } from 'rxjs/Observable';
import 'rxjs/add/operator/delay';
import 'rxjs/add/observable/of';

@Injectable()
export class PlatService {

  constructor() { }

  getPlats(): Observable<Plat[]> {
    return Observable.of(PLATS).delay(2000);
  }

  getPlat(id: number): Observable<Plat> {
    return Observable.of(PLATS.filter((plat) => (plat.id === id))[0]).delay(20)
  }

  getFeaturedPlat(): Observable<Plat> {
    return Observable.of(PLATS.filter((plat) => plat.featured)[0]).delay(20);
  }
}
```
Update all the components as follows to subscribe to the observable returned from the service:
```javascript
this.platService.getPlats().subscribe(plats => this.plats = plats);
```
Update plat.service.ts by adding the following method to the service:
```javascript
 getPlatIds(): Observable<number[]> {
    return Observable.of(PLATS.map(plat => plat.id ));
  }
```
Update the detail-plat.component.ts as follows:
```javascript
import 'rxjs/add/operator/switchMap';
import { Params } from '@angular/router';

prev: number;
next: number;

 ngOnInit() {
    this.platService.getPlatIds().subscribe(platIds => this.platIds = platIds);
    this.route.params
      .switchMap((params: Params) => this.platService.getPlat(+params['id']))
      .subscribe(plat => { this.plat = plat; this.setPrevNext(plat.id); });
  }

  setPrevNext(platId: number) {
    let index = this.platIds.indexOf(platId);
    this.prev = this.platIds[(this.platIds.length + index - 1)%this.platIds.length];
    this.next = this.platIds[(this.platIds.length + index + 1)%this.platIds.length];
  }
```
Update detail-plat.component.html as follows:
```javascript
<mat-card-actions>
       <button mat-button [routerLink]="['/detailPlat', prev]"><span class="fa fa-chevron-left fa-lg"></span></button>
       <button mat-button>LIKE</button>
       <button mat-button>SHARE</button>
       <button mat-button (click)="goBack()">BACK</button>
       <span class="flex-spacer"></span>
       <button mat-button [routerLink]="['/detailPlat', next]"><span class="fa fa-chevron-right fa-lg"></span></button>
</mat-card-actions>
```
Installing json-server :
```javascript
npm install json-server -g
```
Configuring the Server :

At any convenient location on your computer, create a new folder named json-server, and move to this folder.
Download the db.json file provided above to this folder.
Move to this folder in your terminal window, and type the following at the command prompt to start the server:
```javascript
json-server --watch db.json
json-server --watch db.json -d 2000
```
Configuring the Base Server URL :

You need to import the HttpModule in app.module.ts.
```javascript
import { HttpModule } from '@angular/http';

@NgModule({
  
  . . . 
  imports: [ 
    . . . 

    HttpModule 
  ], 
  
  . . .

```
Create a new file named baseurl.ts in the shared folder and update its contents as follows:
```javascript
export const baseURL = 'http://localhost:3000/';
```
 import baseURL and update the AppModule's providers property of the @NgModule decorator as follows:
 ```javascript
 import { baseURL } from './shared/baseurl';
. . .

providers: [
  . . .
  {provide: 'BaseURL', useValue: baseURL}
  ]
```
Create a new service named ProcessHTTPMsg in the services folder.
Open process-httpmsg.service.ts and update its contents as follows:
```javascript
. . .

import { Observable } from 'rxjs/Observable';
import { Http, Response } from '@angular/http';

. . .


  public extractData(res: Response) {
    let body = res.json();
    console.log(body);
    return body || { };
  }
  
  . . .
```
Open plat.service.ts file and update its contents as follows:
```javascript
import { Http, Response } from '@angular/http';
import { baseURL } from '../shared/baseurl';
import { ProcessHttpmsgService } from './process-httpmsg.service';
import 'rxjs/add/operator/catch';
import 'rxjs/add/operator/map';

 constructor(private http: Http,
    private processHttpmsgService: ProcessHttpmsgService) { }
    
 getPlats(): Observable<Plat[]> {
    return this.http.get(baseURL + 'plats')
                    .map(res => { return this.processHttpmsgService.extractData(res); });
  }

  getPlat(id: number): Observable<Plat> {
    return  this.http.get(baseURL + 'plats/'+ id)
                    .map(res => { return this.processHttpmsgService.extractData(res); });
  }

  getFeaturedPlat(): Observable<Plat> {
    return this.http.get(baseURL + 'plats?featured=true')
                    .map(res => { return this.processHttpmsgService.extractData(res)[0]; });
  }

  getPlatIds(): Observable<number[]> {
    return this.getPlats()
      .map(plats => { return plats.map(plat => plat.id) });
  }   

```
Open menu.component.ts and update it as follows:
```javascript
 import { Component, OnInit, Inject } from '@angular/core';
 
 constructor(private platService: PlatService,@Inject('BaseURL') private BaseURL) { }
```

Open menu.component.html and update it as follows:
```javascript
 <img height="200px" src="{{BaseURL + plat.image}}" alt={{plat.name}}>
```
Update process-httpmsg.service.ts to include a function to handle errors as follows:
```javascript
. . .

import 'rxjs/add/observable/throw';


. . .


  public handleError (error: Response | any) {
    // In a real world app, you might use a remote logging infrastructure
    let errMsg: string;
    if (error instanceof Response) {
      const body = error.json() || '';
      const err = body.error || JSON.stringify(body);
      errMsg = `${error.status} - ${error.statusText || ''} ${err}`;
    } else {
      errMsg = error.message ? error.message : error.toString();
    }
    console.error(errMsg);
    return Observable.throw(errMsg);
  }
  . . .
```
Update plat.service.ts to catch and handle errors as follows:
```javascript
. . .
import 'rxjs/add/operator/catch';

. . .
  getPlats(): Observable<Plat[]> {
    return this.http.get(baseURL + 'plats')
                    .map(res => { return this.processHttpmsgService.extractData(res); })
                    .catch(error => { return this.processHttpmsgService.handleError(error); });
  }

  getPlat(id: number): Observable<Plat> {
    return  this.http.get(baseURL + 'plats/'+ id)
                    .map(res => { return this.processHttpmsgService.extractData(res); })
                    .catch(error => { return this.processHttpmsgService.handleError(error); });
  }

  getFeaturedPlat(): Observable<Plat> {
    return this.http.get(baseURL + 'plats?featured=true')
                    .map(res => { return this.processHttpmsgService.extractData(res)[0]; })
                    .catch(error => { return this.processHttpmsgService.handleError(error); });
  }

  getPlatIds(): Observable<number[]> {
    return this.getPlats()
      .map(plats => { return plats.map(plat => plat.id) })
      .catch(error => { return Observable.of(error); });
      
  }
 
```
Update menu.component.ts as follows to handle errors:
```javascript
this.platService.getPlats().subscribe(plats => this.plats = plats,
      errmess => this.errMess = <any>errmess);
```
Update menu.component.html file as follows:
```javascript
<div [hidden]="plats || errMess">
      <mat-spinner></mat-spinner><h4>Loading . . . Please Wait</h4>
    </div>
    <div *ngIf="errMess">
      <h2>Error</h2>
      <h4>{{errMess}}</h4>
    </div>
```
### Building and Deploying the Angular Application

You will note that the build process indicates an error in the Login component. Update the login.component.ts file as follows:
```javascript
  user = {username: '', password: '', remember: false};
```
To build the distribution folder containing your angular application, type the following at the prompt:
```javascript
ng build --target=production
```
Copy the contents of the dist folder to the public folder of your json-server.
Now your Angular application can be accessed at the link http://localhost:3000/

### Angular and REST

First install Ngx-Restangular into your Angular application using NPM as follows:
```javascript
npm install --save ngx-restangular
```
Add a file named restConfig.ts to the shared folder and update its contents as follows:
```javascript
import { baseURL } from './baseurl';

// Function for settting the default restangular configuration
export function RestangularConfigFactory (RestangularProvider) {
  RestangularProvider.setBaseUrl(baseURL);
}
```
Open app.module.ts and update it as follows:
```javascript
. . .
import { RestangularModule, Restangular } from 'ngx-restangular';
import { RestangularConfigFactory } from './shared/restConfig';

. . . 

imports: [
  . . .
  RestangularModule.forRoot(RestangularConfigFactory)
  ]
  . . .
```
Open plat.service.ts and update it as follows to make it use ng2-restangular:

```javascript
. . .
import { RestangularModule, Restangular } from 'ngx-restangular';

. . .
  constructor(private restangular: Restangular,
              private processHTTPMsg: ProcessHTTPMsg) { }
  
    constructor(private restangular: Restangular,
    private processHttpmsgService: ProcessHttpmsgService) { }

  getPlats(): Observable<Plat[]> {
    return this.restangular.all('plats').getList();
  }

  getPlat(id: number): Observable<Plat> {
    return  this.restangular.one('plats',id).get();
  }

  getFeaturedPlat(): Observable<Plat> {
    return this.restangular.all('plats').getList({featured: true})
      .map(plats => plats[0]);
  }

  getPlatIds(): Observable<number[]> {
    return this.getPlats()
      .map(plats => { return plats.map(plat => plat.id) })
      .catch(error => { return Observable.of(error); });
      
  }
```
### Adding a New Directive
```javascript
ng g directive directives/highlight
```
Update highlight.directive.ts file as follows:
```javascript
import { Directive, ElementRef, Renderer2, HostListener  } from '@angular/core';
. . .


  constructor(private el: ElementRef,
    private renderer: Renderer2) { }

  @HostListener('mouseenter') onMouseEnter() {
    this.renderer.addClass(this.el.nativeElement, 'highlight');
  }

  @HostListener('mouseleave') onMouseLeave() {
    this.renderer.removeClass(this.el.nativeElement, 'highlight');
  }
  
  . . .
```
Open styles.scss and add a new scss class to it as follows:
```javascript
$background-pale: #D1C4E9;

 . . .
 
 .highlight {
  background-color: $background-pale;
  border: 1px solid $primary-color-dark;
  z-index: 1;
  transform: scale(1.01);
}
```
Now open menu.component.html and add the new directive as follows:
```javascript
 <mat-grid-tile *ngFor="let plat of plats" [routerLink]="['/detailPlat', plat.id]" appHighlight>
```

