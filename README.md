# FluentAPI

## Basics
<pre>
public class PlutoContext : DbContext
{
  protected override void OnModelCreating(DbModelBuilder modelBuilder)
  {
    modelBuilder.Entity<Course>
          .Property(t => t.Name)
          .IsRequired();
  }
}
</pre>

## Tables
<pre>
Entity<Course>.ToTable(“tbl_Course”, “catalog”);
</pre>

## Primary Keys
<pre>
Entity<Book>.HasKey(t => t.Isbn);

Entity<Book>.Property(t => t.Isbn)
        .HasDatabaseGeneratedOption(DatabaseGeneratedOption.None);
</pre>

## Composite Primary Keys
<pre>
Entity<OrderItem>.HasKey(t => new
            {
              t.OrderId,
              t.OrderId
            });
</pre>

## Columns
<pre>
Entity<Course>.Property(t => t.Name)
        .HasColumnName(“sName”)
        .HasColumnType(“varchar”)
        .HasColumnOrder(2)
        .IsRequired()
        .HasMaxLength(255);
</pre>

## One-to-many Relationship
<pre>
Entity<Author>.HasMany(a => a.Courses)
        .WithRequired(c => c.Author)
        .HasForeignKey(c => c.AuthorId);
</pre>
        
## Many-to-many Relationship
<pre>
Entity<Course> .HasMany(c => c.Tags)
        .WithMany(t => t.Courses)
        .Map(m => {
              m.ToTable(“CourseTag”);
              m.MapLeftKey(“CourseId”);
              m.MapRightKey(“TagId”);
        });
</pre>

## One-to-zero/one Relationship
<pre>
Entity<Course>.HasOptional(c => c.Caption)
        .WithRequired(c => c.Course);
</pre>

## One-to-one Relationship
<pre>
Entity<Course>.HasRequired(c => c.Cover)
        .WithRequiredPrincipal(c => c.Course);
Entity<Cover>.HasRequired(c => c.Course)
        .WithRequiredDependent(c => c.Cover);
</pre>
