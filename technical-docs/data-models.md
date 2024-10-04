---
title: Datenmodell
parent: Technical Docs
nav_order: 2
layout: home
---

# Datenmodell für die Neighbor-App

Dieses Dokument beschreibt das Datenmodell der Neighbor-App, basierend auf SQLAlchemy-Tabellenstrukturen. Die Anwendung verwendet eine relationale Datenbank, um Benutzer, Werkzeuge, Ausleihhistorie und andere relevante Informationen zu speichern.

# Benutzer (User)
Repräsentiert die Nachbarn, die Werkzeuge ausleihen oder verleihen.

```python
class User(UserMixin, db.Model):
    id = db.Column(db.Integer, primary_key=True)
    username = db.Column(db.String(80), nullable=False, unique=True)
    email = db.Column(db.String(120), unique=True, nullable=False)
    password_hash = db.Column(db.String(128), nullable=False)
    rank = db.Column(db.String(50), nullable=True)

    # Beziehungen
    tools = db.relationship('Tool', backref='owner', cascade="all, delete-orphan", lazy=True)
    borrowing_history = db.relationship('BorrowingHistory', backref='borrower', cascade="all, delete-orphan", lazy=True)
    lent_tools = db.relationship('BorrowingHistory', backref='lender', cascade="all, delete-orphan", lazy=True)
    friends = db.relationship('User', secondary='user_friends', backref='added_by')

class Tool(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    name = db.Column(db.String(100), nullable=False)
    description = db.Column(db.Text, nullable=True)
    availability = db.Column(db.String(50), nullable=False)
    available_from = db.Column(db.Date, nullable=False)
    available_until = db.Column(db.Date, nullable=False)
    condition = db.Column(db.String(50), nullable=True)
    deposit_required = db.Column(db.Float, default=0.0)
    owner_id = db.Column(db.Integer, db.ForeignKey('user.id'), nullable=False)
    borrowed_by_id = db.Column(db.Integer, db.ForeignKey('user.id'), nullable=True)

class BorrowingHistory(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    borrow_date = db.Column(db.DateTime, default=datetime.utcnow)
    return_date = db.Column(db.DateTime, nullable=True)

    tool_id = db.Column(db.Integer, db.ForeignKey('tool.id'), nullable=False)
    borrower_id = db.Column(db.Integer, db.ForeignKey('user.id'), nullable=False)
    lender_id = db.Column(db.Integer, db.ForeignKey('user.id'), nullable=False)


class Favorite(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    user_id = db.Column(db.Integer, db.ForeignKey('user.id'), nullable=False)
    tool_id = db.Column(db.Integer, db.ForeignKey('tool.id'), nullable=True)
    neighbor_id = db.Column(db.Integer, db.ForeignKey('user.id'), nullable=True)

class Rating(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    rating = db.Column(db.Integer, nullable=False)
    comment = db.Column(db.Text, nullable=True)
    rater_id = db.Column(db.Integer, db.ForeignKey('user.id'), nullable=False)
    ratee_id = db.Column(db.Integer, db.ForeignKey('user.id'), nullable=False)
    tool_id = db.Column(db.Integer, db.ForeignKey('tool.id'), nullable=True)

class SecurityDeposit(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    amount = db.Column(db.Float, nullable=False)
    tool_id = db.Column(db.Integer, db.ForeignKey('tool.id'), nullable=False)

class Tool(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    name = db.Column(db.String(100), nullable=False)
    description = db.Column(db.Text, nullable=True)
    availability = db.Column(db.String(50), nullable=False)
    available_from = db.Column(db.Date, nullable=False)
    available_until = db.Column(db.Date, nullable=False)
    condition = db.Column(db.String(50), nullable=True)
    deposit_required = db.Column(db.Float, default=0.0)
    owner_id = db.Column(db.Integer, db.ForeignKey('user.id'), nullable=False)
    borrowed_by_id = db.Column(db.Integer, db.ForeignKey('user.id'), nullable=True)

user_friends = db.Table('user_friends',
    db.Column('user_id', db.Integer, db.ForeignKey('user.id')),
    db.Column('friend_id', db.Integer, db.ForeignKey('user.id'))
)


