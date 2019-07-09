# processing_templates

TODO: 桜吹雪でマウスを押すと背景が白くなっていきキーボードを押すと背景が黒くなっていく

## Usage

TODO: 実行ボタンを押して背景を白くしたければマウスを押し、黒くしたければキーボードを押す

## Code review

TODO:
``` java
ArrayList<Triangle> triangles;
float add;
float bcolor;

void setup(){
  size(640, 480, P3D);
  noStroke();
  fill(255, 230, 234);
  triangles = new ArrayList<Triangle>();
}

void mousePressed(){
   add += 10;
}
void keyPressed(){
  add -= 10; 
}
void draw(){ 
  
  background (bcolor+add);
  ArrayList<Triangle> nextTriangles = new ArrayList<Triangle>();
  for(Triangle t: triangles){
    t.display();
    t.update();
    if(t.loc.y < height + 200){
      nextTriangles.add(t);
    }
  }
  triangles = nextTriangles;
  if(random(1) < noise(frameCount * 0.001 + 100000)){
    triangles.add(new Triangle());
  }
}
class Triangle{
  
  float size = 20;
  PVector loc, lvel;
  PVector rot, rvel;

Triangle(){
    loc = new PVector(map(noise(frameCount * 0.01), 0, 1, 0, width), -50, random(-30, 30) - 50);
    lvel = new PVector(0, 0, 0);
    rot = new PVector(random(TWO_PI), random(TWO_PI), random(TWO_PI));
    rvel = new PVector(0, 0, 0);
  }

void display(){
    pushMatrix();
    translate(loc.x, loc.y, loc.z);
    rotateX(rot.x);
    rotateY(rot.y);
    rotateZ(rot.z);
    beginShape();
    vertex(size * cos(0), size * sin(0), 0);
    vertex(size * cos(PI * 1.0 / 3), size * sin(PI * 1.0 / 3), 0);
    vertex(size * cos(PI * 2.0 / 3), size * sin(PI * 2.0 / 3), 0);
    endShape(CLOSE);
    popMatrix();
  }
  void update(){
    lvel.add(new PVector(random(-0.1, 0.1), 0, random(-0.1, 0.1)));
    lvel.x = constrain(lvel.x, -1, 1);
    lvel.z = constrain(lvel.z, -1, 1);
    loc.add(lvel);
    loc.y += random(0, 1);
    rvel.add(new PVector(random(-PI / 128, PI / 128), random(-PI / 128, PI / 128), random(-PI / 128, PI / 128)));
    rvel.x = constrain(rvel.x, -PI / 32, PI / 32);
    rvel.y = constrain(rvel.x, -PI / 32, PI / 32);
    rvel.z = constrain(rvel.x, -PI / 32, PI / 32);
    rot.add(rvel);
  }
}
```

アニメが好きで一番好きなアニメシーンを真似てみたかったから
https://www.openprocessing.org/sketch/380934
このcodeを引用した
## License

ここではサンプルとしてMITライセンスの表示をしています．Creative commonsとかLGPLでもOKです．
[Githubのライセンシングを解説した記事](https://www.catch.jp/oss-license/2013/09/10/github/)は
とても参考になります(だいぶその時...2013か...からは改訂されてるけど)．

The processing application is available as open source under the terms of the [MIT License](https://opensource.org/licenses/MIT).

## Code of Conduct

Everyone interacting in the Test project’s codebases, issue trackers, chat rooms and mailing lists is expected to follow the [code of conduct](https://github.com/[USERNAME]/processing_templates/blob/master/CODE_OF_CONDUCT.md).
