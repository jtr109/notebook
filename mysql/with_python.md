# MySQL With Python

## 1 SQLAlchemy

## 2 Flask-SQLAlchemy

### 2.1 Model Relationships

**One-to-Many Relationships**


    # One side:
    ...
    addresses = db.relationship('Address', backref='person',
        lazy='dynamic')
    ...
    
    # Many side:
    ...
    person_id = db.Column(db.Integer, db.ForeignKey('person.id'))
    ...

**Many-to-Many Relationships**

    tags = db.Table('tags',
        db.Column('tag_id', db.Integer, db.ForeignKey('tag.id')),
        db.Column('page_id', db.Integer, db.ForeignKey('page.id'))
    )
    
    class Page(db.Model):
        id = db.Column(db.Integer, primary_key=True)
        tags = db.relationship('Tag', secondary=tags,
            backref=db.backref('pages', lazy='dynamic'))
    
    class Tag(db.Model):
        id = db.Column(db.Integer, primary_key=True)
        
_注意：多对多关系中，建立`Table`连接两个模型，在其中一侧声明`db.relationship`，其中`backref=db.backref('...', lazy= '...')。和一对多中不同。_

### 2.2 Session

对象只有在`commit`之后才会获得id
