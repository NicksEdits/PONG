#include <Grapic.h>
#include <iostream>
#include <math.h>
#include <cmath>

using namespace grapic;
using namespace std;

const int DIMW=500;
const float  dt=2;
const short STARS = 100;

//création des complexes
struct Complex
{
    float x,y;
};
Complex make_complex(float r, float i)
{
    Complex c;
    c.x = r;
    c.y = i;
    return c;
}
Complex operator+(Complex a, Complex b)
{
    Complex c = make_complex( a.x+b.x, a.y+b.y );
    return c;
}

Complex operator-(Complex a, Complex b)
{
    Complex c = make_complex( a.x-b.x, a.y-b.y );
    return c;
}
Complex operator*(float a, Complex b)
{
    Complex c = make_complex( a*b.x, a*b.y );
    return c;
}
Complex operator/(Complex b, float d)
{
    Complex c = make_complex( b.x/d, b.y/d );
    return c;
}
struct casse_bar
{
    Complex bar;
    Complex bar2;
    Image  imbar;
    Image  imbar2; // image de la bar
    Complex stars[STARS];//tableau de petites étoiles pour un fond plus presentable
};
struct vec
{
    float x;
    float y;
};
vec make_vec(float x, float y)
{
    vec v;
    v.x = x;
    v.y = y;
    return v;
}
struct Particles{
    vec p; //postion
    vec v; //vitesse
    vec f; //force
    float m; //masse
};
struct World
{
    Particles tab[DIMW];
    int n; // le nombre de particules
    int score1;
    int score2;

};


// Les operateurs:
vec operator+(vec a, vec b)
{
    vec c;
    c.x=a.x+b.x; c.y=a.y+b.y;
    return c;
}
vec operator-(vec a, vec b)
{
    vec c;
    c.x=a.x-b.x; c.y=a.y-b.y;
    return c;
}
vec operator*(vec a,float b)
{
    vec c;
    c.x=a.x*b; c.y=a.y*b;
    return c;
}
vec operator*(vec a,vec b)
{
    vec c;
    c.x=a.x*b.x-a.y*b.y; c.y=a.x*b.y+a.y*b.x;
    return c;
}
vec operator/(vec a,float b)
{
    vec c;
    c.x=a.x/b; c.y=a.y/b;
    return c;
}

void AddForce(Particles & p, vec f)
{
    p.f=p.f+f; //ajoute la force au vecteur force de la particule
}
void Gravity(Particles& p,World & dat)
{


;if(dat.tab[0].p.x < 250){p.f = p.f + make_vec(0,-p.m*0.1f );}
if(dat.tab[0].p.x > 250){p.f = p.f + make_vec(0,-p.m*-0.05f );}

}
void update(Particles & p, float dt)
{
   vec f= p.f;
    p.p=p.p + p.v*dt; //mise à jour de la position
    p.v=(p.f/p.m)*dt+p.v;  //mise à jour de la vitesse

}
void update2(Particles & p, float dt,World & dat)
{
   vec f= p.f;
    p.p=p.p + p.v*dt; //mise à jour de la position
    p.v=(p.f/p.m)*dt+p.v;  //mise à jour de la vitesse

    Gravity(p,dat); // ajoute de la gavité
}

//l'initialisation data/PONG/bar_pong.png
void init(World & dat , casse_bar& b)
{
    dat.n=1; //le nombre de balles pour plusieurs niveaux de difficultés
    b.bar= make_complex(DIMW/2+30, DIMW/2+30); // creation de la barre de droite
    b.imbar = image("data/bar_pong.png");
    b.bar2= make_complex(DIMW/2 -450, DIMW/2 -250); // creation de la barre de gzuche
    b.imbar2 = image("data/bar_pong.png");
    vec g;g.x=0;g.y=-9.81;



    for (int i = 0; i < STARS; ++i) {
    b.stars[i] = make_complex(rand() % DIMW, rand() % DIMW); //creation des etoiles
  }


}
void init_balle(World &dat)
{

     dat.score1 = -1;
     dat.score2 = 0;
 for (int i=0;i<dat.n;i++)
 {


       dat.tab[i].p.x=frand(250,250);
       dat.tab[i].p.y=frand(0,-200);
       dat.tab[i].m=frand(1,20);
       dat.tab[i].v.x=dt*150;
       dat.tab[i].v.y=dt*1;
       dat.tab[i].f.x=0;
       dat.tab[i].f.y=0;
 }
}
/*void reset(Particles &p, score &s)
{
   // s.score1=0;
  //  s.score2=0;


       p.p.x=frand(250,250);
       p.p.y=frand(0,-200);
       p.m=1.0;
       p.v.x=dt*50;
       p.v.y=dt*50;
       p.f.x=0;
       p.f.y=0;

}*/


void draw(World & dat , casse_bar& b,int w,int x,int c)
{
    //les petites etoiles
    for (int i = 2; i < STARS; ++i) {
    color(255, 255, 255, 200);

     circleFill(b.stars[i].x, b.stars[i].y,rand()% 3);
    point(b.stars[i].x, b.stars[i].y);
  }

    image_draw(b.imbar2 , b.bar2.x +200   ,b.bar2.y  ,20,130);
    image_draw(b.imbar , b.bar.x +200   ,b.bar.y  ,20,130);
    for(int i=0;i<dat.n;i++)
    {
        color(w,x,c);
        circleFill(dat.tab[i].p.x,dat.tab[i].p.y,8.5);
    }
    fontSize(15);

 rectangle(65,448,41,475);
  rectangle(440,448,465,475);
     print(50, 450, dat.score1);
    print(450, 450, dat.score2);



if(dat.score1<0)
{
    print(150,450,"Press 'F1' to hide the menue");
    print(175,430,"The first has 10 win");
}
if(dat.score2>5)
{

    dat.tab[0].p.x=250;
    dat.tab[0].p.y=250;

    fontSize(25);
    print(135,255,"RIGHT PLAYER WIN");
    fontSize(15);
    print(120,220,"Press 'ENTER' to restart or 'ESC' to quit");
    if ((isKeyPressed(SDLK_KP_ENTER))||(isKeyPressed( SDLK_RETURN)))
    {
        init_balle(dat);

    }
}
if(dat.score1>5)
{
    dat.tab[0].p.x=250;
    dat.tab[0].p.y=250;
    fontSize(25);

    print(135,255,"LEFT PLAYER WIN");
    fontSize(15);
    print(120,220,"Press 'ENTER' to restart or 'ESC' to quit");
    if ((isKeyPressed(SDLK_KP_ENTER))||(isKeyPressed( SDLK_RETURN)))
    {
        init_balle(dat);

    }
}



}
void update_world(World & dat , casse_bar& b)
{
   int score=0; //pour initialiser le score qui sera implementé plus tard
      int z= 0;
    int e= 0;
    int r= 0;
    int w=255;
    int x = 255;
    int c = 255;




        backgroundColor(z,e,r); // pour faire un mode jour et un mode nuit


    for (int i=0;i<dat.n;i++)
    {
        update(dat.tab[i],0.001);

if (dat.tab[i].p.x >= b.bar.x+200 && dat.tab[i].p.y >= b.bar.y && dat.tab[i].p.y < b.bar.y+130) //collision de la balle avec la barre de droite
        {
                dat.tab[i].v.x=-dat.tab[i].v.x*1.3;         // augmentation de la vitesse de la balle après collision sur la bar pour plus de difficultés

                if (dat.tab[i].v.x *1.2 < -2050)                   //limitation de la vitesse pour que le jeu reste jouable.
                {
                        dat.tab[i].v.x= dat.tab[i].v.x / 1.4;

                }
        }
 if (dat.tab[i].p.x-220 <= b.bar2.x && dat.tab[i].p.y >= b.bar2.y-20 && dat.tab[i].p.y < b.bar2.y+150) //collision de la balle avec la barre de gauche
        {
                dat.tab[i].v.x=-dat.tab[i].v.x;      // augmentation de la vitesse de la balle après la collision sur la barre pour plus de difficulté
        }




       if (dat.tab[i].p.y>500 || dat.tab[i].p.y<0) //collision avec le mur
           dat.tab[i].v.y=-dat.tab[i].v.y;




        if (dat.tab[i].p.x > 500)//cas ou le joueur rate la balle
           {
                dat.tab[i].p.x=frand(200,300);
                dat.tab[i].p.y=frand(0,500);
                dat.tab[i].v.x=dt*50;
                dat.tab[i].v.y=dt*50;
                 dat.score1++;

           }
 if (dat.tab[i].p.x < -20)  //cas ou le joueur rate la balle
           {
                dat.tab[i].p.x=frand(200,300);
                dat.tab[i].p.y=frand(500,0);
                dat.tab[i].v.x=dt*50;
                dat.tab[i].v.y=dt*50;
                 dat.score2++;

           }
    }
     const float d = 0.8f;
    if (isKeyPressed(SDLK_UP))      // bouger la bar
    {
        if (b.bar.y < DIMW) b.bar.y+=d;
        if (b.bar.y > DIMW-130) b.bar.y=DIMW-130;

    }
    if (isKeyPressed(SDLK_DOWN))
    {
        if (b.bar.y <0)b.bar.y=-b.bar.y*d;
        if (b.bar.y > 0) b.bar.y-=d;
    }
    if (isKeyPressed('z'))      // bouger la bar
    {
        if (b.bar2.y < DIMW) b.bar2.y+=d;
        if (b.bar2.y > DIMW-130) b.bar2.y=DIMW-130;

    }
    if (isKeyPressed('s'))
    {
        if (b.bar2.y <0)b.bar2.y=-b.bar2.y*d;
        if (b.bar2.y > 0) b.bar2.y-=d;
    }

}


void update_world2(World & dat , casse_bar& b)
{
   int score=0; //pour initialiser le score qui sera implementé plus tard
      int z= 0;
    int e= 0;
    int r= 0;
    int w=255;
    int x = 255;
    int c = 255;




        backgroundColor(z,e,r); // pour faire un mode jour et un mode nuit


    for (int i=0;i<dat.n;i++)
    {
        update2(dat.tab[i],0.001,dat);

if (dat.tab[i].p.x >= b.bar.x+200 && dat.tab[i].p.y >= b.bar.y && dat.tab[i].p.y < b.bar.y+130) //collision de la balle avec la barre de droite
        {
                dat.tab[i].v.x=-dat.tab[i].v.x*1.5;         // augmentation de la vitesse de la balle après collision sur la bar pour plus de difficultés

                if (dat.tab[i].v.x *1.2 < -1650)                   //limitation de la vitesse pour que le jeu reste jouable.
                {
                        dat.tab[i].v.x= dat.tab[i].v.x / 1.4;

                }
        }
 if (dat.tab[i].p.x-220 <= b.bar2.x && dat.tab[i].p.y >= b.bar2.y-20 && dat.tab[i].p.y < b.bar2.y+150) //collision de la balle avec la barre de gauche
        {
                dat.tab[i].v.x=-dat.tab[i].v.x*1.2;      // augmentation de la vitesse de la balle après la collision sur la barre pour plus de difficulté
        }




       if (dat.tab[i].p.y>500 || dat.tab[i].p.y<0) //collision avec le mur
           dat.tab[i].v.y=-dat.tab[i].v.y;




        if (dat.tab[i].p.x > 500)//cas ou le joueur rate la balle
           {
                dat.tab[i].p.x=frand(200,300);
                dat.tab[i].p.y=frand(250,500);
                dat.tab[i].v.x=dt*100;
                dat.tab[i].v.y=dt*100;
                 dat.score1++;

           }
 if (dat.tab[i].p.x < -20)  //cas ou le joueur rate la balle
           {
                dat.tab[i].p.x=frand(200,300);
                dat.tab[i].p.y=frand(500,250);
                dat.tab[i].v.x=dt*100;
                dat.tab[i].v.y=dt*100;
                 dat.score2++;

           }
    }
     const float d = 0.4f;
    if (isKeyPressed(SDLK_UP))      // bouger la bar
    {
        if (b.bar.y < DIMW) b.bar.y+=d;
        if (b.bar.y > DIMW-130) b.bar.y=DIMW-130;

    }
    if (isKeyPressed(SDLK_DOWN))
    {
        if (b.bar.y <0)b.bar.y=-b.bar.y*d;
        if (b.bar.y > 0) b.bar.y-=d;
    }
    if (isKeyPressed('z'))      // bouger la bar
    {
        if (b.bar2.y < DIMW) b.bar2.y+=d;
        if (b.bar2.y > DIMW-130) b.bar2.y=DIMW-130;

    }
    if (isKeyPressed('s'))
    {
        if (b.bar2.y <0)b.bar2.y=-b.bar2.y*d;
        if (b.bar2.y > 0) b.bar2.y-=d;
    }

}


int main(int , char **)
{

    bool stop=false;
    casse_bar b;
    winInit("Pong",500,500);
    World dat ;

    Particles p;
    init(dat , b);
    init_balle(dat);
    Menu menu;
    menu_add(menu, "Play");
    menu_add(menu, "Pause");  //ajout d'une option pause qui stop le jeux jusqua appuyer sur le menue play
    menu_add(menu, "Restart");
    menu_add(menu, "Gravity ");
    menu_setSelect(menu,0);
     int w,x,c;
    w=255;
    x=255;
    c=255;

    backgroundColor(20,90,60);
    while (!stop)
    {
        setKeyRepeatMode(true);
        winClear();
         menu_draw(menu,35 ,15, 100, 100);
        switch(menu_select(menu))
        {
            case 0 : dat.n = 1; update_world(dat, b);draw(dat , b,w,x,c); break;
            case 1 : dat.n = 1;   draw(dat , b,w,x,c); fontSize(70);
            print(138,220,"PAUSE"); break;
            case 2 : dat.n = 1;init_balle(dat);menu_setSelect(menu,0); break;
            case 3 : dat.n = 1; update_world2(dat, b);draw(dat , b,w,x,c); break;

            default: dat.n=0; draw(dat , b,w,x,c); break;
        }

      //  draw(dat , b,w,x,c);
      //  update_world(dat,b);

        stop = winDisplay();
    }
    winQuit();
    return 0;
}
